Now to create a new cookie, we need a method that will add this cookie to our `_cookies` state. So we will create a method that takes the new cookie as an argument add it to `_cookies` and pass this method as a prop down to our modal.

1. In `App.js`, let's create our method `createCookie` that takes `newCookie` as an argument:

```javascript
const createCookie = (newCookie) => {};
```

2. How can we update a state that's an array? We can do it the long way:

```javascript
const createCookie = (newCookie) => {
  const updatedCookies = _cookies;
  updatedCookies.push(newCookie);
  setCookies(updatedCookies);
};
```

3. Let's try this method out first, pass it as a prop to `CookieList`:

```jsx
<CookieList
  cookies={_cookies}
  createCookie={createCookie}
  deleteCookie={deleteCookie}
/>
```

4. De-structure `props` in `CookieList`:

```javascript
const CookieList = ({ cookies, createCookie, deleteCookie }) => {
```

5. Pass `createCookie` again to `CookieModal`:

```jsx
<CookieModal
  isOpen={isOpen}
  closeModal={closeModal}
  createCookie={createCookie}
/>
```

6. De-structure `props` in `CookieModal`:

```javascript
const CookieModal = ({ isOpen, closeModal, createCookie }) => {
```

7. Pass the method to `handleSubmit`:

```javascript
const handleSubmit = (event) => {
  event.preventDefault();
  createCookie(cookie);
};
```

8. Let's try it out. Nope, it's not working!

9. So we can pass `setCookies` a de-structured array `_cookies` and `newCookie` added to it.

```javascript
const createCookie = (newCookie) => {
  setCookies([..._cookies, newCookie]);
};
```

10. Much cleaner! And let's try it out. Yes! It's working.

11. But now, we want our modal to close automatically after creating a cookie. We can easily call `closeModal` in `handleSubmit`

```javascript
const handleSubmit = (event) => {
  event.preventDefault();
  createCookie(cookie);
  closeModal();
};
```
