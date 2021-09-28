Let's create an update button in our cookie item component that opens the modal.

1. In `styles.css`, create a class called `update-button`

```css
.update-button {
  color: #ff85a2;
}
```

2. Create a new component called `UpdateButton`, use `update-button` and render it:

```javascript
import React from 'react';

const UpdateButton = () => {
  return <button className="update-button">Update</button>;
};

export default UpdateButton;
```

3. Also we will use it and render our modal. Wrap the two components with a fragment `<> </>`

```javascript
// Components
import CookieModal from '../modals/CookieModal';

const UpdateButton = () => {
  return (
    <>
      <button className="update-button">Update</button>;
      <CookieModal />
    </>
  );
};
```

4. Now `CookieModal` requires a state and method that opens and closes the modal. We'll create a new state, and open and close methods:

```javascript
const UpdateButton = () => {
  const [isOpen, setIsOpen] = useState(false);

  const closeModal = () => setIsOpen(false);

  const openModal = () => setIsOpen(true);
```

5. Pass `isOpen` and `closeModal` to `CookieModal`

```jsx
<CookieModal isOpen={isOpen} closeModal={closeModal} />
```

6. Let's render it in `CookieItem` above the delete button:

```jsx
<UpdateButton  />
<DeleteButton cookieId={cookie.id} />
```

7. Now when clicking on this button, we want to open the modal. Give the `button` an `onClick` event and pass it `openModal`.

```jsx
<button onClick={openModal} className="update-button">
  Update
</button>
```

8. Click on the button, the modal is open! Perfect!
