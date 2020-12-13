Now to create a new cookie, we need a method that will add this cookie to our `cookies` in our store. So we will create a method that takes the new cookie as an argument add it to `this.cookies`.

1. In `cookieStore.js`, let's create our method `createCookie` that takes `newCookie` as an argument:

   ```javascript
   createCookie = (newCookie) => {};
   ```

2. How can we update a state that's an array? We can do it the long way:

   ```javascript
   createCookie = (newCookie) => {
     this.cookies.push(newCookie);
   };
   ```

3. In `CookieModal`, import `cookieStore`:

   ```javascript
   // Stores
   import cookieStore from "../../stores/cookieStore";
   ```

4. Call the method in your `handleSubmit` method:

   ```javascript
   const handleSubmit = (event) => {
     event.preventDefault();
     cookieStore.createCookie(cookie);
   };
   ```

5. Let's try creating a new cookie. Nothing happened..... So weird! Let's console log `cookies` in our method

   ```javascript
   createCookie = (newCookie) => {
     this.cookies.push(newCookie);
     console.log("CookieStore -> createCookie -> this.cookies", this.cookies);
   };
   ```

6. The array is changing! But it's like `CookieList` is not seeing the change. We need Khalty Gmasha's super powers! We need to make `CookieList` an `observer` to track any changes in our store. In `CookieList`, import `observer`:

   ```javascript
   import { observer } from "mobx-react";
   ```

7. Wrap your component in the export line:

   ```javascript
   export default observer(CookieList);
   ```

8. Let's try it out. Yes! It's working.

9. But now, we want our modal to close automatically after creating a cookie. We can easily call `closeModal` in `handleSubmit`

   ```javascript
   const handleSubmit = (event) => {
     event.preventDefault();
     cookieStore.createCookie(cookie);
     closeModal();
   };
   ```
