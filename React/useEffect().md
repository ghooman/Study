## 📌 useEffect()
useEffect 함수는 리액트 컴포넌트가 렌더링 될 때마다 특정 작업을 실행할 수 있도록 하는 Hook이다.   
useEffect는 component가 mount 됐을 때, unmount 됐을 때, update 됐을 때 특정 작업을 처리할 수 있다.   

**✔️ 사용법**
```javascript
useEffect(()=>{ 실행할코드 })  // 1. 렌더링마다 코드를 실행한다.

useEffect(()=>{ 실행할코드 }, [])  // 2. 컴포넌트 mount시(로드시) 1회만 실행 가능하다.

useEffect(()=>{  // 3. useEffect 안의 코드 실행 전에 항상 실행된다. 
  return ()=>{
    실행할코드
  }
})

useEffect(()=>{  // 4. 컴포넌트 unmount시 1회 실행된다.
  return ()=>{
    실행할코드
  }
}, [])

useEffect(()=>{  // 5. state1이 변경될 때만 실행된다.
  실행할코드
}, [state1])
