1. In `CookieDetail`, import `cookieStore`.

```javascript
// Stores
import cookieStore from "../stores/cookieStore";
```

2. Remove `cookies` that's coming from `props` and replace with `cookieStore.cookies`

```javascript
const CookieDetail = () => {
  const { cookieId } = useParams();
  const cookie = cookieStore.cookies.find((cookie) => cookie.id === +cookieId);
```

3. Remove `deleteCookies` that's coming from `props`

```jsx
<DeleteButton cookieId={cookie.id} />
```

4. In `App`, delete `_cookies` and remove the `cookies` import. Also remove `cookies` and `deleteCookies` that you're passing as `props` to `CookieDetail`.

5. Try deleting a cookie from the detail page. It doesn't work?? Well, if you go to the list page, you'll see it's actually been deleted. But when you delete the cookie, the `CookieDetail` component doesn't respond to the change in the data. So we have to *make it an `observer`*.

    Import `observer` in `CookieDetail.js`:

    ```javascript
    import { observer } from "mobx-react";
    ```

    Then set `CookieDetail` as an `observer`:
    
    ```javascript
    export default observer(CookieDetail);
    ```