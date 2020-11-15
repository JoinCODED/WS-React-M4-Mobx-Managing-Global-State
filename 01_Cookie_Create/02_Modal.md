Now when clicking on this button, we want to open a modal. We won't be using bootstrap's modal, instead we will use `react-modal`.

1. Install `react-modal`:

```shell
  $ yarn add react-modal
```

2. Let's take a look at the [documentation](https://www.npmjs.com/package/react-modal). As you can see, a modal needs a state to open and close it. And we need to pass the state and set method to the modal.

3. So lets create our state first in `CookieList`:

```javascript
const [isOpen, setIsOpen] = useState(true);
```

4. Let's also create two methods that open and close the modal by changing the value of `isOpen`:

```javascript
const closeModal = () => setIsOpen(false);

const openModal = () => setIsOpen(true);
```

5. Pass `openModal` to our create button's `onClick` that opens the modal for us:

```jsx
<BsPlusCircle className="float-right" size="2em" onClick={openModal} />
```

6. Now let's create our modal component. Create a new folder called `modals` and a file called `CookieModal`. Setup your component:

```javascript
import React from "react";

const CookieModal = () => {
  return <div></div>;
};

export default CookieModal;
```

7. In `CookieModal`, import `Modal` from `react-modal`.

```javascript
import Modal from "react-modal";
```

8. Render `Modal`, remove `onAfterOpen`.

```javascript
return (
  <Modal
    isOpen={}
    onRequestClose={}
    style={customStyles}
    contentLabel="Example Modal"
  >
    <h3>New Cookie</h3>
  </Modal>
);
```

9. As you can see we need to pass `isOpen` and `closeModal` as `props`. So go back to `CookieList`, and pass them.

```jsx
<CookieModal isOpen={isOpen} closeModal={closeModal} />
```

10. Pass `isOpen` and `closeModal` to `Modal`.

```jsx
<Modal
  isOpen={showModal}
  onRequestClose={closeModal}
  style={customStyles}
  contentLabel="Cookie Modal"
>
  <h3>New Cookie</h3>
</Modal>
```

11. Let's try out our modal. Yay It's working!
