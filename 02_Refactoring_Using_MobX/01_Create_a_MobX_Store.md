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

6. Now we turn this class into a store that can manage the changes in `cookies`. To do that we will import `decorate` and `observable` from `mobx`:

```javascript
import { decorate, observable } from "mobx";
```

7. Now **after** defining our class we will call the `decorate` method and pass it our class, `CookieStore`. This method `decorates` `CookieStore` by giving it the superpowers that will turn it to a mobx store.

```javascript
class CookieStore {
  cookies = cookies;
}

decorate(CookieStore);
```

8. Also, decorate takes an object. In this object we will define our properties that can be observed by the app's components. If a property is defined as an observable, the components can see the changes that occur to it.

```javascript
class CookieStore {
  cookies = cookies;
}

decorate(CookieStore, {
  cookies: observable,
});
```

9. Next we need to create an instance of our store and export it:. Keep in mind that if you export it without creating an instance, any component that imports it will have its own instance!

```javascript
const cookieStore = new CookieStore();
export default cookieStore;
```

10. Let's use our new store!
