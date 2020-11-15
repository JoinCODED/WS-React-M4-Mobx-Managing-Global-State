In this lesson, we will create more cookies. We will have a create button, when pressing on it, it will open a modal that has a form.

1. Let's add a plus icon in our list page. But how can we add icons? We will use a library called [React Icons](https://react-icons.github.io/react-icons/). Let's install it.

```shell
  $ yarn add react-icons
```

2. Let's try it out, first choose your icon and import it:

```javascript
import { BsPlusCircle } from "react-icons/bs";
```

3. Then you simply render it as a component:

```jsx
<ListWrapper className="row">{cookieList}</ListWrapper>
<BsPlusCircle />
```

4. But it's size is very small, let's style it! According to the [documentation](https://github.com/react-icons/react-icons#configuration), all icons have a `prop` called `size` and the default is `1em`. So let's change it to `2em`. We'll also give it a `float-right` class to change its position.

```jsx
<BsPlusCircle className="float-right" size="2em" />
```

5. And our button is ready!
