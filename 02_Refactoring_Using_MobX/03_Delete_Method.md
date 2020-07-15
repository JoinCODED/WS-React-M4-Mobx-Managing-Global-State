1. Now let's move the `deleteCookie` to our lovely store. Remove the `setCookies` line and directly update `this.cookies`

```javascript
deleteCookie = (cookieId) => {
  this.cookies = this.cookies.filter((cookie) => cookie.id !== cookieId);
};
```

2. Go to `DeleteButton` component, import `cookieStore`:

```javascript
import cookieStore from "../../stores/cookieStore";
```

3. Replace `deleteCookie` from `props` with `cookieStore.deleteCookie`

```javascript
const handleDelete = (event) => {
  event.preventDefault();
  cookieStore.deleteCookie(cookieId);
};
```

4. Try the delete button. It's working!

5. Delete both `_cookies` state and `deleteCookie` method in `App`, `CookieList`, `CookieItem`, `DeleteButton` and `CookieDetail`. The code looks much better!!
