Let's create our update method

1. In `cookieStore`, create a method that takes a cookie as an argument and for now let's just log it out.

```javascript
updateCookie = (updatedCookie) => {
  console.log("CookieStore -> updateCookie -> updatedCookie", updatedCookie);
};
```

2. Let's try to call it in `CookieModal`. But we already have a `handleSubmit` that calls `createCookie`! We will add a conditional operator, if `oldCookie` exists we will call `updateCookie`, else we will call `createCookie`. In both cases we will pass `cookie`.

```javascript
const handleSubmit = (event) => {
  event.preventDefault();
  cookieStore[oldCookie ? "updateCookie" : "createCookie"](cookie);
  closeModal();
};
```

3. Also, let's fix the submit button to render `Update` if `oldCookie` exists.

```jsx
<CreateButtonStyled className="btn float-right" type="submit">
  {oldCookie ? "Update" : "Create"}
</CreateButtonStyled>
```

4. Let's call `updateCookie`. Yes! It's working. Now, how can we actually update our cookie in our list of cookies?

5. Let's start by finding the cookie that has the `updatedCookie.id` using `.find`.

```javascript
updateCookie = (updatedCookie) => {
  console.log("CookieStore -> updateCookie -> updatedCookie", updatedCookie);
  const cookie = this.cookies.find((cookie) => cookie.id === updatedCookie.id);
};
```

What makes `.find` so cool is the fact that it returns the actual element from the array not a copy of it. So, if we change the properties in `cookie` the change will be applied in the array. How cool is that?

But keep in mind one thing! If you override it by saying `cookie = updatedCookie` the connection will be lost. So we will manually change the properties.

6. We will overwrite all the properties in `cookie` with the properties coming from `updatedCookie`. You'll see that the values changed in `cookies` as well!

```javascript
updateCookie = (updatedCookie) => {
  const cookie = this.cookies.find((cookie) => cookie.id === updatedCookie.id);
  cookie.name = updatedCookie.name;
  cookie.price = updatedCookie.price;
  cookie.image = updatedCookie.image;
  console.log("updateCookie -> cookie", cookie);
};
```

7. Since we're updating data in the store, let's set the `updateCookie` method as an `action` in the `constructor`.

```javascript
constructor() {
  makeObservable(this, {
    cookies: observable,
    createCookie: action,
    updateCookie: action,
    deleteCookie: action,
  })
}
```

7. Let's test it out. Nothing happened. That's because `CookieItem` must be an `observer`. Import `observer`

```javascript
import { observer } from "mobx-react";
```

8. Wrap `CookieItem` with `observer`

```javascript
export default observer(CookieItem);
```

9. Let's try it again. It's working!!!

10. But the code is so ugly! To clean it up, we will loop over our `cookie` object and only replace the properties that exist in `updatedCookie`. Let's take a look at the [documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in) first.

```javascript
updateCookie = (updatedCookie) => {
  const cookie = this.cookies.find((cookie) => cookie.id === updatedCookie.id);
  for (const key in cookie) cookie[key] = updatedCookie[key];
};
```

11. Let's also update the slug of the cookie, in case the name of the cookie was updated.

```javascript
updateCookie = (updatedCookie) => {
  const cookie = this.cookies.find((cookie) => cookie.id === updatedCookie.id);
  for (const key in cookie) cookie[key] = updatedCookie[key];
  cookie.slug = slugify(cookie.name);
};
```

12. Try it again. Yup, it's working perfectly.
