Before adding our form, let's clean our code. Let's move the add button and modal into their own component.

1. Create a new component in `buttons` called `AddButton`.

```javascript
import React from "react";

const AddButton = () => {
  return <div></div>;
};

export default AddButton;
```

2. Move the add button and modal to `AddButton` and wrap them with a fragment. Don't forget to move the imports as well.

```jsx
<>
  <BsPlusCircle className="float-right" size="2em" onClick={openModal} />
  <CookieModal isOpen={isOpen} closeModal={closeModal} />
</>
```

3. Move the `isOpen` state and methods

```javascript
const [isOpen, setIsOpen] = useState(true);

const closeModal = () => setIsOpen(false);

const openModal = () => setIsOpen(true);
```

4. Now render `AddButton` in `CookieList`.

```jsx
<AddButton />
```

Wow! Much cleaner.
