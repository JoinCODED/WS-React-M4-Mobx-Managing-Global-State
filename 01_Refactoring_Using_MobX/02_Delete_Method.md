Now, instead of passing `cookies` as a prop to `CookieList` and `CookieDetail`, we can directly import our store in those components and access the data directly!

1. In `CookieList`, import `cookieStore`:

```javascript
// Stores
import cookieStore from "../stores/cookieStore";
```

2. To access `cookies` in `cookieStore`, we will say `cookieStore.cookies`. So let's replace `cookies` that's coming from `props` with `cookieStore.cookies`.

3. Let's see what happens. Our cookies are there! But the delete method stopped working, because they're updating the cookies state not the store cookies.

4. Now let's move the `deleteCookie` to our lovely store. Remove the `setCookies` line and directly update `this.cookies`.

   ```javascript
   deleteCookie = (cookieId) => {
     this.cookies = this.cookies.filter((cookie) => cookie.id !== cookieId);
   };
   ```

5. Go to `DeleteButton` component, import `cookieStore`:

   ```javascript
   import cookieStore from "../../stores/cookieStore";
   ```

6. Replace `deleteCookie` from `props` with `cookieStore.deleteCookie`

   ```javascript
   const handleDelete = (event) => {
     event.preventDefault();
     cookieStore.deleteCookie(cookieId);
   };
   ```

7. Try the delete button. It's working!

8. Delete both `_cookies` state and `deleteCookie` method in `App`, `CookieList`, `CookieItem`, `DeleteButton` and `CookieDetail`. The code looks much better!!
