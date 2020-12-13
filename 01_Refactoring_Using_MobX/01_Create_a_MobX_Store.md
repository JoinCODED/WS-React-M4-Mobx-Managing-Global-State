At this point, our code is growing, and the code in `App` is becoming bulkier. Also, passing `cookies` and its methods can easily become messier. So we will create a store that manages our global data.

1. Start with installing `mobx` and `mobx-react`.

```shell
  $ yarn add mobx mobx-react
```

2. Create a folder in `src` called `stores`. This is where we will create all our application's stores.

3. Create a file called `cookieStore.js`.

4. A store is simply a `class`. Let's define our class:

```javascript
class CookieStore {}
```

5. What are our properties? Or what's the data that's being used by many components? In this case it's `cookies`. So we'll import it in and save it in a class property:

```javascript
import cookies from "../cookies";

class CookieStore {
  cookies = cookies;
}
```

6. Now we turn this class into a store that can manage the changes in `cookies`. To do that we will import `makeAutoObservable` and `observable` from `mobx`:

```javascript
import { makeAutoObservable, observable } from "mobx";
```

7. Next, we need to define a constructor for our class, and call `makeAutoObservable` inside, and pass it `this`. This'll give our class `CookieStore` the superpowers of a MobX store.

```javascript
class CookieStore {
  cookies = cookies;

  constructor() {
    makeAutoObservable(this);
  }
}
```

8. Next we need to create an instance of our store and export it. If we just export the class, it won't work like we expect it to.

```javascript
const cookieStore = new CookieStore();
export default cookieStore;
```

9. Let's use our new store!
