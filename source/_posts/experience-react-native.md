---
title: Những kinh nghiệm với React Native trong 6 tháng
thumbnail: https://c1.staticflickr.com/4/3947/33288549710_b91a7c7403_k.jpg
tags: react native
---
![](https://c1.staticflickr.com/4/3947/33288549710_b91a7c7403_k.jpg)

Bài viết dành cho những người đã hiểu sơ qua về React-Native. Bài này sẽ nói lên kinh nghiệm React Native theo góc nhìn của mình. Nếu bài viết của mình có gì sai sót hay thiếu sót, các bạn có thể comment ở phía dưới để mình tiện chỉnh sửa. Mình cảm ơn nhiều.

## Vòng đời sống trong react-native
![Life Cycle React Native](https://cdn-images-1.medium.com/max/1600/0*VoYsN6eq7I_wjVV5.png)
Hình phía trên là miêu tả một quá trình mà react-native gọi lần lượt các hàm.
Như trên thì RN(react-native) gọi hàm getDefaultProps() đầu tiên, rồi đến getInitialState(),.. rồi theo trình tự như vậy.

**Ở đây bạn chú ý:**
**1.** Mọi hoạt động trên native dựa vào `state` tức có nghĩa là mỗi khi `state` thay đổi thì RN sẽ gọi hàm render lại. Hay nói cách khác bạn hãy sử dụng 4 khốn khéo ở `state` để hạn chế hay muốn re-render lại Component. Vì sao lại hạn chế? Nếu bạn sử dụng `state` 1 cách bừa bãi, điều này sẽ ảnh hưởng tới hiệu năng ứng dụng của bạn. Làm cho ứng dụng bạn phải cực nhọc re-render liên tục. Bạn phải cân nhắc component nào thì render, component nào không, hay component nào là luôn luôn không. Dựa vào `PureComponent` trong RN.
`PureComponent` giúp ta kiểm tra props trước và props hiện tại có giống nhau không. Nếu giống thì sẽ không re-render lại.
**Ví dụ:**      
Mình có app như thế này
https://github.com/tomzaku/Calculator-React-Native-Simple
![](https://camo.githubusercontent.com/03143983d4ea418ac4141c0b1e6fbaca14727684/687474703a2f2f7376312e757073696575746f632e636f6d2f323031362f31322f31362f53637265656e53686f74323031362d31322d31366174392e34372e3330414d2e706e67)

Nhìn trên thì bạn có thể thấy các button (AC, /, X , - +,=,1,2,3,4,5,6,7,8,9,0,00,.) hầu như không thây đổi gì cả trong quá trình ứng dụng nên mình sẽ sử dụng `PureComponent` cho button ấy
Nên khi mình re-render lại component, RN sẽ nhận biết không cần render lại nữa.

**Code:**

https://github.com/tomzaku/Calculator-React-Native-Simple/blob/master/src/components/Button.js#L10-L20
```javascript
export default class Button extends React.PureComponent {
  constructor(props) {
    super(props);
  }

 onPress=()=>{
   const {onPress,title} = this.props;
   if (onPress) {
    onPress(title);
    }
  }
 }
```

**2.** Ở trên sẽ có hàm shouldComponentUpdate(nextProps,nextState). Hàm này sẽ phát hiện sự thay đổi của props (thường thì compoent cha thay đổi state ảnh hưởng tới compoent con, hoặc từ `redux`). Từ phát hiện thay đổi props này, các bạn có thể thay đổi state để re-render lại compoent như mình mong muốn
Ví dụ :

...Continue


## Cấu trúc thư mục ntn
...Continue
## Tăng hiệu năng RN
...Continue

## Test
...Continue

## Theme như thế nào để linh hoạt và thuận tiện
...Continue

## Thư viện nào mình đang dùng
...Continue
