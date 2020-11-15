To create a cookie form we need 4 fields, `name`, `description`, `price` and `image`.

1. So let's set our `form` tags and inside it add our `input` tags

```jsx
<form>
  <input />
  <input />
  <input />
  <input />
</form>
```

2. Now to make styling easier, I will use Bootstrap. I've prepared the following form:

```jsx
<form>
  <div className="form-group row">
    <div className="col-6">
      <label>Name</label>
      <input className="form-control" />
    </div>
    <div className="col-6">
      <label>Price</label>
      <input className="form-control" />
    </div>
  </div>
  <div className="form-group">
    <label>Description</label>
    <input className="form-control" />
  </div>
  <div className="form-group">
    <label>Image</label>
    <input className="form-control" />
  </div>
</form>
```

3. Now we need to set the type of each input field to prevent the user from writing strings in the price field for example. To do that, we will use the attribute `type`. `name`, `description` and `image` are supposed to be of type `text` and `price` is of type `number`. Keep in mind that our images at this point are image addresses or URLs:

```jsx
<form>
  <div className="form-group row">
    <div className="col-6">
      <label>Name</label>
      <input type="text" className="form-control" />
    </div>
    <div className="col-6">
      <label>Price</label>
      <input type="number" className="form-control" />
    </div>
  </div>
  <div className="form-group">
    <label>Description</label>
    <input type="text" className="form-control" />
  </div>
  <div className="form-group">
    <label>Image</label>
    <input type="text" className="form-control" />
  </div>
</form>
```

4. Let's try it out. Now for the price field, we will set the minimum value to `1` so that we don't get a `0` or a negative number:

```jsx
<input type="number" min="1" className="form-control" />
```

5. Our form is ready!

6. So now we need to capture the user's input and save it. So we will create an object state that has a property for every field.

```javascript
const [cookie, setCookie] = useState({
  name: "",
  price: 0,
  description: "",
  image: "",
});
```

7. Create a function that will handle the change in the `name` field. Basically we will de-structure our `cookie` object and overwrite the `name` field:

```javascript
const handleChange = (event) => {
  setCookie({ ...cookie, name: event.target.value });
};
```

8. Pass the function to the `name`'s input field:

```jsx
<input type="text" className="form-control" onChange={handleChange} />
```

8. But are we gonna do this for all our input fields? There is an easier way, first we will add give a `name` to every `input` tag. Take care that the name must be the same as the key in the `cookie` state:

```jsx
<input
  type="text"
  className="form-control"
  name="name"
  onChange={handleChange}
/>
```

```jsx
<input type="text" className="form-control" name="description" />
```

9. In `handleChange`, instead of adding an if-condition that checks the name of the input field, we will make our key dynamic:

```javascript
const handleChange = (event) => {
  setCookie({ ...cookie, [event.target.name]: event.target.value });
};
```

10. So now whenever the user types in anything in any field, it's being saved into our component's state.

11. Let's add a `Create` button. In `styles`:

```
export const CreateButtonStyled = styled.button`
  color: ${(props) => props.theme.backgroundColor};
  background-color: ${(props) => props.theme.mainColor};

  &:hover {
    color: ${(props) => props.theme.mainColor};
    background-color: ${(props) => props.theme.backgroundColor};
  }
`;
```

12. Import `CreateButtonStyled` in `CookieModal`, and place it at the end of the form.

```jsx
<CreateButtonStyled className="btn float-right">Create</CreateButtonStyled>
</form>
```

13. Now let's create our function that will pass this object to `cookies`. For now let's just console.log it:

```javascript
const handleSubmit = () => {
  console.log(cookie);
};
```

14. We will use a new event called `onSubmit`. `onSubmit` can be triggered when we click on our button, or when we even just press on the enter key!

15. The `onSubmit` method is added to the `form` tag.

```jsx
 <form onSubmit={handleSubmit}>
```

16. Let's try submitting it. Oops, the page is being refreshed. That's because `onSubmit`'s default behavior is refreshing the page. We can easily prevent that by using the `preventDefault` method:

```javascript
const handleSubmit = (event) => {
  event.preventDefault();
  console.log(cookie);
};
```

17. Let's try again. Yaay it's working!
