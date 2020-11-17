Now, instead of passing `cookies` as a prop to `CookieList` and `CookieDetail`, we can directly import our store in those components and access the data directly!

1. In `CookieList`, import `cookieStore`:

```javascript
// Stores
import cookieStore from "../stores/cookieStore";
```

2. To access in `cookies` in `cookieStore`, we will say `cookieStore.cookies`. So let's replace `cookies` that's coming from `props` with `cookieStore.cookies`:

3. Let's see what happens. Our cookies are there! But the delete and create stopped working, because they're updating the cookies state not the store cookies.

4. Let's move the `createCookie` method to the store and fix it. Don't forget to move the `slugify` import as well.

5. First, remove the method's `const` and replace `_cookies` with `cookies`:

```javascript
createCookie = (cookie) => {
  cookie.id = cookies[cookies.length - 1].id + 1;
  cookie.slug = slugify(cookie.name);
  setCookies([...oldCookies, cookie]);
};
```

6. In a mobx store we're dealing with normal properties, so we don't need set methods. We can directly change `cookies`. But remember! In a class, to refer to one of its properties we need to use `this`!

```javascript
createCookie = (cookie) => {
  cookie.id = this.cookies[this.cookies.length - 1].id + 1;
  cookie.slug = slugify(cookie.name);
  this.cookies.push(cookie);
};
```

7. This method is used in `CookieModal`, so we will import it there:

```javascript
// Stores
import cookieStore from "../../stores/cookieStore";
```

8. Replace `createCookie` with `cookieStore.createCookie`:

```javascript
const handleSubmit = (event) => {
  event.preventDefault();
  cookieStore.createCookie(cookie);
  closeModal();
};
```

9. Let's try creating a new cookie. Nothing happened..... So weird! Let's console log `cookies` in our method

```javascript
createCookie = (newCookie) => {
  newCookie.id = this.cookies[this.cookies.length - 1].id + 1;
  newCookie.slug = slugify(newCookie.name);
  this.cookies.push(newCookie);
  console.log("CookieStore -> createCookie -> this.cookies", this.cookies);
};
```

10. The array is changing! But it's like `CookieList` is not seeing the change. We need Khalty Gmasha's super powers! We need to make `CookieList` an `observer` to track any changes in our store. In `CookieList`, import `observer`:

```javascript
import { observer } from "mobx-react";
```

11. Wrap your component in the export line:

```javascript
export default observer(CookieList);
```

12. Well... it's still not updating! There's one more thing we need to do... We need to set the `createCookie` function as an `action` in the store.

    Import `action` in `cookieStore.js`:

    ```javascript
    import { makeObservable, observable, action } from "mobx";
    ```

    Then set `createCookie` as an `action`:

    ```javascript
    constructor() {
      makeObservable(this, {
        cookies: observable,
        createCookie: action,
      })
    }
    ```

13. Now we can remove `createCookie` from `App`, `CookieList` and `CookieModal`! A HUUUUGEE TARARARAAAAAAA!!!
