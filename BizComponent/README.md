## 简介
本组件库有三大组件，分别是地址拖拽以及切换组件、图片轮播组件以及数字键盘组件。

1，地址交换组件的功能  
地址添加：允许跳转到地图带回目标数据，包括地址名称、联系人和电话号码。  
地址排序：用户可以通过拖拽的方式重新排序地址列表，方便调整地址的顺序。  
地址交换：用户可以选择两个地址进行交换，改变它们在列表中的位置。  
地址删除：用户可以删除不需要的地址。
### 效果展示：
![img.png](
https://mdapcdn.huolala.cn/devops/mdap2/harmony_address_1cc4f6df674546e7764e758ef2296982.gif)

```


OpenHarmony ohpm 环境配置等更多内容，请参考[如何安装 OpenHarmony ohpm 包](https://gitee.com/openharmony-tpc/docs/blob/master/OpenHarmony_har_usage.md)

## 使用说明

```ets
import {
  AddressComponent,
  CommonComponentUIBean,
  StandardAddressBeanArray,
  StandardOrderAddressBean
} from 'lib_addresscomponent'


@Entry
@Component
export struct Test {
   /**
   * 地址列表数据源
   */
  @State addressArray: StandardAddressBeanArray = new StandardAddressBeanArray()
   /**
   * 地址列表UI
   */
  @State commonUIBean: CommonComponentUIBean = new CommonComponentUIBean()

  aboutToAppear(): void {
    this.initData()
    this.initUI()
  }

  build() {
    Column() {
      Blank().layoutWeight(1)
      AddressComponent({
        addressArray: this.addressArray,
        onAddAddressClick: () => {
          this.testAddData()
        },
        commonUIBean: this.commonUIBean
      })
      Blank().layoutWeight(1)
    }
  }

  /**
   * 测试添加地址
   */
  testAddData() {
    let addressArray = this.addressArray
    let length = addressArray.length
    let addBean = new StandardOrderAddressBean(length - 1, "新地址名称", "131XXXX6789")
    addressArray.splice(length - 1, 0, addBean)
    addressArray[length].index = length
  }

  /**
   * 初始化地址
   */
  initData() {
    for (let i = 0; i < 2; i++) {
      let name = `序列号${i}地址`
      let phone = `${i}123456789`
      let bean = new StandardOrderAddressBean(i, name, phone)
      this.addressArray.push(bean)
    }
  }

  /**
   * 自定义UI
   */
  initUI() {
    this.commonUIBean.nameColor = $r('app.color.client_orange')
    this.commonUIBean.dragText = "滑动"
  }
}
```
## 属性说明
1. AddressComponent：地址列表外层组件
2. DragAddressList：两个地址以上的地址列表组件，可以拖动和删除
3. NormalAddressList：两个地址的地址列表组件，可以交换起始地址和结束地址
4. CommonComponentUIBean：自定义地址列表的UI参数

| 属性                   | 类型                          | 释义                               | 默认值        |
| ---------------------- | ----------------------------- | ---------------------------------- |------------|
| changeAddressIcon               | Resource                        |交换地址的icon                       | -          |
| changeIconWidth            | number                        | 交换地址的宽度                          | 23         |
| changeIconHeight               | number                        | 交换地址的高度                         | 23         |
| changeIconPadding  | number                        | 交换地址的padding            | 6.5        |
| startPointColor         | ResourceColor                      |起点的颜色                 | 0x000000   |
| passingPointColor                | ResourceColor                        |途经点的颜色                      | 0x40000000 |
| endPointColor              | ResourceColor                        | 终点的颜色 | 0xFFFF6600 |
| passingAddressIcon             | Resource                        | 途经点的icon              | -          |
| passingText               | string                        |途经点文案             | 途经点        |
| pointWidth                  | number                        | 圆点宽度                | 7          |
| pointHeight              | number                        |圆点高度             | 7          |
| nameColor           | ResourceColor                       | 地址名的颜色             | 0xB3000000 |
| nameFontSize           | number                       |地址名字体大小   | 14         |
| nameMaxLines | number                       |  地址名最多显示几行                    | 1          |
| nameImageIcon              | Resource                       | 地址名右箭头的icon      | -          |
| nameImageIconWidth                | number                       | 地址名右箭头的宽度                      | 12         |
| nameImageIconHeight          | number                       |  地址名右箭头的高度                  | 12         |
| phoneFontSize    | number | 电话字体大小         | 12         |
| phoneColor   | ResourceColor | 电话的颜色          | 0x73000000 |
| dragText   | string | 拖动文案          | 拖动         |
| dragImageIcon   | Resource | 拖动的icon          | -          |
| deleteImageIcon   | Resource | 删除的icon          | -          |

2，图片轮播组件的功能  
自动播放：轮播组件可以在指定的时间间隔后自动切换图片，提供动态的用户体验。  
手动导航：用户可以通过导航控件（如左右的缩略图）手动浏览图片。  
过渡效果：可以应用各种过渡效果（如淡入淡出、滑动或缩放）来增强视觉吸引力。  
图片说明：每张图片可以附带说明或描述，提供额外的上下文或信息。  
事件回调：开发者可以在各种事件（如图片切换或导航点击）中挂钩自定义逻辑或分析。  
多轮播支持：支持在同一页面上使用多个轮播组件，每个组件都有自己的设置和内容。
### 效果展示：
![img.png](
https://mdapcdn.huolala.cn/devops/mdap2/harmony_%20carousel_054d4901931b454ff2fbe1a02144f2bf.gif)

```

## 使用说明

```ets
import {
  SelSwiperTabSource,
  SwiperImageArray,
  SwiperImageComponent,
  SwiperImageUiBean
} from "lib_swiperpicturescomponent"


@Entry
@Component
export struct Test2 {
  /**
   * 图片列表数据源
   */
  @State swiperImageArray: SwiperImageArray = new SwiperImageArray()
  
  /**
   * 当前选中的vehicleIndex
   */
  @State currentImageIndex: number = 0

  aboutToAppear(): void {
    this.testAddData(1,
      "https://luna-cdn-public-test.huolala.cn/luna-public-al-test/test001/900900/20230921/1001d9256507ac074e17a70242eda6fb8aed.png")
    this.testAddData(2,
      "https://luna-cdn-public-test.huolala.cn/luna-public-al-test/test001/900900/20230921/1001358c9e7e595c49588850292b8c418e03.png")
    this.testAddData(3,
      "https://luna-cdn-public-test.huolala.cn/luna-public-al-test/test001/900900/20230921/1001851b397b6a8644e1bb7a037ee5e8a01a.png")
    this.testAddData(4,
      "https://luna-cdn-public-test.huolala.cn/luna-public-al-test/test001/900900/20230921/1001ed957fb6906d4c1c8f1479baa2554510.png")
    this.testAddData(5,
      "https://luna-cdn-public-test.huolala.cn/luna-public-al-test/test001/900900/20230921/1001a30936c51ace4a2abc42cc014f9b85c7.png")
  }

  build() {
    Column() {
      Blank().layoutWeight(1)
      SwiperImageComponent({
        imagesArray: this.swiperImageArray,
        currentImageIndex: this.currentImageIndex,
        indexChangeAction: (source: SelSwiperTabSource, index: number) => {

        },
        onImageClick: (imageBean: SwiperImageUiBean) => {
        }
      })
      Blank().layoutWeight(1)
    }.padding({ bottom: 12 })

  }

  /**
   * 添加图片测试数据
   */
  testAddData(swiperId: number, imageUrl: string) {
    let addBean = new SwiperImageUiBean()
    addBean.swiperId = swiperId
    addBean.imageUrl = imageUrl
    this.swiperImageArray.push(addBean)
  }

}



```
## 属性说明
1. SwiperImageComponent：图片轮播组件
2. SwiperComponentUIBean：自定义图片轮播组件的UI参数

| 属性                   | 类型                          | 释义                               | 默认值        |
| ---------------------- | ----------------------------- | ---------------------------------- |------------|
| altImage               | Resource                        |滚动的默认图片                       | -          |

3，数字键盘组件的功能  
数字输入：允许用户轻松输入数字，通常包括0-9的数字键。  
退格/删除：包括一个键用于删除最后输入的数字，允许用户纠正错误。  
确认/提交：具有确认或提交按钮，用于确认输入，常用于表单或计算器。  
事件回调：允许开发者在按键、释放键和输入提交等事件中挂钩自定义逻辑。  
### 效果展示：
![img.png](
https://mdapcdn.huolala.cn/devops/mdap2/harmony_keypad_c72f076c092f8d2d0fe0a0b605d0c652.gif)

```

## 使用说明

```ets
import { DialogNumberKeyboard } from 'lib_numberkeyboard';
import { StringUtil } from '../utils/StringUtil';

@Entry
@Component
export struct Test3 {
  /**
   * 最终数字结果
   */
  @State inputText: string = ''

  /**
   * 自定义键盘
   */
  @Builder
  dialogNumberKeyboardBuilder() {
    DialogNumberKeyboard({
      //number==-2时，则就是删除功能
      onNumberClick: (number: number) => {
        this.handleKeyboardInput(number)
      },
    })
      .width('100%')
      .height(220)
  }

  build() {
    Stack() {
      Row() {
        Text("我的出价").fontSize(16).fontColor($r('app.color.black_85_percent')).margin({ left: 16 })
        TextInput({ text: this.inputText, placeholder: '请输入价格' })
          .caretColor($r('app.color.client_orange'))
          .backgroundColor(Color.Transparent)
          .placeholderColor($r('app.color.gray_25_percent'))
          .fontColor($r('app.color.black_85_percent'))
          .fontSize(22)//.maxLength(10)
          .layoutWeight(1)
          .padding({ right: 8 })
          .height(44)
          .margin({ left: 12 })
          .textAlign(TextAlign.End)//.defaultFocus(true)
          .customKeyboard(this.dialogNumberKeyboardBuilder(), { supportAvoidance: true })
          .type(InputType.Number)
          .onChange((value) => {
            this.inputText = value
            this.onTextChange(value)
          })
          .onTouch((event: TouchEvent | undefined) => {

          })

        Text('元')
          .width(40)
          .fontSize(16)
          .fontColor($r('app.color.black_65_percent'))
      }
      .height(52)
      .margin({ bottom: 10 })
      .backgroundColor(0XF3F4F5)
      .borderRadius(8)

    }
    .margin({ top: 12, left: 16, right: 16 })
    .alignContent(Alignment.TopEnd)

  }

  /**
   * 处理键盘输入
   * @param input
   */
  private handleKeyboardInput(input: number) {
    if (StringUtil.isNullOrEmpty(this.inputText) && input >= 0) {
      this.inputText = input.toString()
      return
    }
    //删除事件
    if (input < 0) {
      if (!StringUtil.isNullOrEmpty(this.inputText)) {
        this.inputText = this.inputText.substring(0, this.inputText.length - 1)
      }
      return
    }
    this.inputText += input
  }

  /**
   * 监听文本变化
   * @param text
   */
  private onTextChange(text: string) {
    try {
      if (StringUtil.isNullOrEmpty(text)) {
      } else {
        if (text.length == 1 && text == ("0")) {
          this.inputText = ''
          return
        }
      }
    } catch (err) {
    }
  }
}



```
## 属性说明
1. DialogNumberKeyboard：数字键盘组件

## 约束与限制

在以下版本验证通过：

- DevEco Studio: 4.1 Canary(4.1.3.500), SDK: API11 (4.1.0)
- DevEco Studio: 4.1 Canary(4.1.3.700), SDK: API11 (4.1.0)

## 贡献代码

使用过程中发现任何问题都可以提 Issue 给我们，当然，我们也非常欢迎你给我们发 PR 。
