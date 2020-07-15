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
