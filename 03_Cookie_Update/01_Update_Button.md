Let's create an update button in our cookie item component that opens the modal.

1. In `styles.js`, create a styled component called `UpdateButtonStyled`

```javascript
export const UpdateButtonStyled = styled.p`
  color: ${(props) => props.theme.pink};
`;
```

2. Create a new component called `UpdateButton`, import `UpdateButtonStyled` and render it:

```javascript
import React from "react";

// Styling
import { UpdateButtonStyled } from "../../styles";

const UpdateButton = () => {
  return <UpdateButtonStyled>Update</UpdateButtonStyled>;
};

export default UpdateButton;
```

3. Also we will import and render our modal. Wrap the two components with a fragment `<> </>`

```javascript
// Components
import CookieModal from "../modals/CookieModal";

const UpdateButton = () => {
  return (
    <>
      <UpdateButtonStyled>Update</UpdateButtonStyled>
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

7. Now when clicking on this button, we want to open the modal. Give `UpdateButtonStyled` an `onClick` event and pass it `openModal`.

```jsx
<UpdateButtonStyled onClick={openModal}>Update</UpdateButtonStyled>
```

8. Click on the button, the modal is open! Perfect!
