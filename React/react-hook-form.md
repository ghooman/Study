## 📌 React Hook Form
React Hook Form은 React에서 Form을 쉽게 만들기 위한 라이브러리이다.   
공식 문서에는 유연하고 확장 가능한 사용하기 쉬운 고성능 폼 검증 라이브러리라고 설명되어 있다.

### ✔️ 설치
```
npm install react-hook-form
```

### ✔️ 예제
```javascript
import React from "react";
import { useForm } from "react-hook-form";

export default function App() {
  const { register, handleSubmit, watch, formState: { errors } } = useForm();
  const onSubmit = data => console.log(data);

  console.log(watch("example")); // watch input value by passing the name of it

  return (
    /* "handleSubmit" will validate your inputs before invoking "onSubmit" */
    <form onSubmit={handleSubmit(onSubmit)}>
      {/* register your input into the hook by invoking the "register" function */}
      <input defaultValue="test" {...register("example")} />
      
      {/* include validation with required or other standard HTML validation rules */}
      <input {...register("exampleRequired", { required: true })} />
      {/* errors will return when field validation fails  */}
      {errors.exampleRequired && <span>This field is required</span>}
      
      <input type="submit" />
    </form>
  );
}
```
