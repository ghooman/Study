## 📌 extends
extends는 클래스의 자식 클래스를 생성할 때 사용한다.
```javascript
class World {
    constructor(nation){
        this.nation = nation;
    }

    whereRUFrom(){
        console.log(`I'm from ${this.nation}.`);
    }
}

class Asia extends World {
    constructor(nation){
        super(nation);
    }
    whereRUFrom(){
        console.log(`I live in ${this.nation}.`)
    }
}

let imfrom = new Asia('SouthKorea');
imfrom.whereRUFrom();
//"I live in SouthKorea."
```

super()는 부모 생성자를 호출한다.   
부모 생성자의 일이 끝난 후 부모가 해결하지 못하는 것은 자식 생성자가 하도록 하는 것이다.   
이 super()가 없다면 중복이 될 것을 부모에게 가서 실행시키고 오는것이다.   

World라는 클래스를 사용 하면서 거기서 더 부가적인 기능을 추가해서 이용하고 싶을 때 extends, 상속을 이용한다.   
물론 World 클래스에서 다른 메소드를 넣을 수 있으나, 만일 저 코드가 내 코드가 아니거나 수정하면 참 곤란해지는 것 이라면, 신경쓸게 많아질 것이다.   
때문에 어차피 겹치게 될 World의 생성자를 상속받고 나머지는 자식인 Asia의 whereRUFrom만 호출하여 결국 자식의 콘솔로그만 출력이 되는 것이다.
