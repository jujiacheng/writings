# redux

## 基础使用

1. 新建models文件夹，创建actions，reducers文件夹
2. actions文件夹内新建user.ts

```TypeScript
export const updateUserInfo = (data: any) => {
  return {
    type: "updateUserInfo",
    data,
  };
};
```

1. reducers文件夹下新建user.ts

```TypeScript
export default (state = "", action: { type: string; data: any }) => {
  console.log(state);
  switch (action.type) {
    case "updateUserInfo":
      return action.data;
      break;
    default:
      return state;
      break;
  }
};
```

1. reducers文件夹下新建index.ts

```TypeScript
import { combineReducers } from "redux";
import user from "./user";
export default combineReducers({
  user,
});
```

1. models下新建index.ts

```TypeScript
import { createStore, applyMiddleware } from "redux";
import { composeWithDevTools } from "@redux-devtools/extension";
import thunkMiddleware from "redux-thunk";
import reducers from "./reducers";
const data = {
  user: {
    id: 1,
    name: "GoodWe",
  },
};

export type ReduxData = typeof data;

export default createStore(
  reducers,
  data,
  composeWithDevTools(applyMiddleware(thunkMiddleware))
);
```

1. 使用

```TypeScript
import React, { useEffect } from "react";
import { Provider } from "react-redux";
import store from "@/models";

export default () => {
  return (
    <Provider store={store}>
      aaa
    </Provider>
  );
};
import React, { useEffect, useState } from "react";
import { useDispatch, useSelector } from "react-redux";
import { updateMessagePoint } from "@/models/actions/message";
const TabsNavigationDemo = (props: PropsWithRoute) => {
  const dispatch = useDispatch();
  /**
  * 消息tab是否需要展示红点
  */
  const messagePoint = useSelector((state: any) => state.message);
  // 初始化页面需要调用一次接口判断消息页面有没有未读消息
  useEffect(() => {
    dispatch(updateMessagePoint(!messagePoint));
  }, []);
  useEffect(() => {
    console.log("aaaa", messagePoint);
  }, [messagePoint]);
  return <div></div>;
};

export default TabsNavigationDemo;
```

### 中间件公式

```
const middleware = store => next => action =>{}
```