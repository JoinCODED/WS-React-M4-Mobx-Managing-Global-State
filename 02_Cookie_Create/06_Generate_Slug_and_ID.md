1. To make an `input` tag required, we basically add the attribute `required`:

   ```javascript
   <input
     required
     name="name"
     type="text"
     className="form-control"
     onChange={handleChange}
   />
   ```

2. To add an ID to our cookie item, we'll basically get the ID of the last item in `this.cookies` and increment it by 1.

   ```javascript
   createCookie = (newCookie) => {
     newCookie.id = this.cookies[this.cookies.length - 1].id + 1;
     this.cookies.push(newCookie);
   };
   ```

3. To add a slug, we will install a library called [`react-slugify`](https://www.npmjs.com/package/react-slugify).

   ```shell
     $ npm install react-slugify
   ```

4. Import `slugify` in `cookieStore.js`

   ```javascript
   import slugify from "react-slugify";
   ```

5. Add a new property to your `newCookie` item called `slug` and pass it the return value of the slugified name

   ```javascript
   createCookie = (newCookie) => {
     newCookie.id = this.cookies[this.cookies.length - 1].id + 1;
     newCookie.slug = slugify(newCookie.name);
     this.cookies.push(newCookie);
   };
   ```
