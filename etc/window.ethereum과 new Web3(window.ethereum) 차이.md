## 📌 window.ethereum과 new Web3(window.ethereum) 차이
`window.ethereum`과 `new Web3(window.ethereum)`는 Ethereum 블록체인과 상호작용하기 위한 두 가지 방법이다.

`window.ethereum`은 Ethereum 클라이언트의 일부로, 대부분의 브라우저에서 지원된다.
이 객체는 DApp에서 Ethereum 블록체인에 접근할 수 있는 API를 제공한다.
`window.ethereum` 객체는 Web3.js 1.0 버전 이후에 추가된 Ethereum Provider API에 기반하여 작동한다.
따라서 DApp에서 Ethereum 블록체인과 상호작용하는 데 사용할 수 있는 Ethereum Provider 인터페이스의 인스턴스를 제공한다.
이 인터페이스는 Ethereum 노드에 JSON-RPC 요청을 보내고 결과를 받는 데 사용된다. (JSON-RPC는 나중에 찾아봐야겠다...)

`new Web3(window.ethereum)`은 Web3.js 라이브러리의 인스턴스를 생성하는 방법 중 하나이다.
Web3.js는 Ethereum 블록체인과 상호작용하기 위한 JavaScript 라이브러리로, Ethereum Provider API를 기반으로 작동한다.
`new Web3(window.ethereum)`을 사용하면 Ethereum 블록체인에 대한 Web3.js 인스턴스를 생성하고, 이를 통해 DApp에서 Ethereum 블록체인과 상호작용할 수 있다.

결론적으로, `window.ethereum`은 Ethereum Provider API의 인스턴스를 제공하고,
`new Web3(window.ethereum)`은 Web3.js의 Ethereum Provider API를 사용하여 Ethereum 블록체인에 대한 인스턴스를 생성한다.
따라서 둘 다 Ethereum 블록체인과 상호작용하는 데 사용될 수 있다.
그러나 `window.ethereum`은 Ethereum Provider API의 인스턴스만 제공하므로, 더 많은 유틸리티 기능을 가진 Web3.js를 사용하려면 `new Web3(window.ethereum)`을 사용해야한다.
