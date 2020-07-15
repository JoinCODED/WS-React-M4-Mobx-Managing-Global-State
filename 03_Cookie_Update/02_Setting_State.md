Now when the modal opens we want the details of the cookie we clicked on to be automatically filled in our fields.

1. To do that we will pass the `cookie` object as a `prop` to the update button then to the modal. In `CookieItem`, pass `cookie` as a `prop` to `UpdateButton`

```jsx
<UpdateButton cookie={cookie} />
```

2. In `UpdateButton`, pass `cookie` as a `prop` to `CookieModal`. Keep in mind that `CookieModal` already has a state called `cookie`. So we will call our prop `oldCookie`

```jsx
<CookieModal isOpen={isOpen} closeModal={closeModal} oldCookie={cookie} />
```

3. Now in `CookieModal`, we will save our `oldCookie` in state.

```javascript
const [cookie, setCookie] = useState({
  name: oldCookie.name,
  price: oldCookie.price,
  description: oldCookie.description,
  image: oldCookie.image,
});
```

But how can we display the state in the fields? Hmmmmm

4. `input` tags have an attribute called `value`, basically we will link our `input` fields to our state:

```jsx
<input
  required
  name="name"
  value={cookie.name}
  type="text"
  className="form-control"
  onChange={handleChange}
/>
```

5. Add a value attribute for all your fields.

6. We got an error! But why?!!

Now keep in mind that we're using `CookieModal` for both the create and update.We got an error because we don't pass `oldCookie` to the modal when we're creating a cookie. So we need a condition, before saving `oldCookie` in our `cookie` state.

7. We will check, if `oldCookie` exists save its values in the state:

```javascript
const [cookie, setCookie] = useState({
  name: oldCookie ? oldCookie.name : "",
  price: oldCookie ? oldCookie.price : 0,
  description: oldCookie ? oldCookie.description : "",
  image: oldCookie ? oldCookie.image : "",
});
```

Let's open the create and update modals. The fields are filled with the cookie we want to update! That's so cool!

8. But the code is a bit repeated. Let's clean it up. If `oldCookie` exists return `oldCookie` else return the object with empty fields

```javascript
const [cookie, setCookie] = useState(
  oldCookie ? oldCookie : {
    name: "",
    price: 0,
    description: "",
    image: "",
  }
```

9. We can clean it up even more!! The `??` basically means that if `oldCookie` exists return `oldCookie` else return the object with empty fields

```javascript
const [cookie, setCookie] = useState( oldCookie ?? {
    name: "",
    price: 0,
    description: "",
    image: "",
  }
```

JavaScript is BOSS wallah!
