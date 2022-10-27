***

<div align=right style="width: 80px"><img src="https://img1.imgtp.com/2022/09/01/IVKUXjNX.gif"></div>



# 事件

常见的事件有：单击、双击、长按、还有触摸事件 。我们可以给文本、按钮等等组件添加不同的事件。

## 单击事件

- 接口名：ClickedListener

四种实现方法(下面的其他事件类推)：

1. 自己编写实现类

```java
public class MainAbilitySlice extends AbilitySlice {

    Button btn1;
    @Override
    public void onStart(Intent intent) {
        super.onStart(intent);
        super.setUIContent(ResourceTable.Layout_ability_main);

        btn1 = (Button) findComponentById(ResourceTable.Id_btn1);

        // 1.自定义实现类
        btn1.setClickedListener(new MyListener());

    }

    @Override
    public void onActive() {super.onActive();}

    @Override
    public void onForeground(Intent intent) {super.onForeground(intent);}
}

// 自定义实现类，里面重写点击方法
class MyListener implements Component.ClickedListener{
    @Override
    public void onClick(Component component) {
        Button btn1 = (Button) component;

        btn1.setText("被点了");

        btn1.setClickable(false);
    }
}
```

2. 实现 Component.ClickedListener 接口

```java
public class MainAbilitySlice extends AbilitySlice implements Component.ClickedListener {

    Button btn1;
    @Override
    public void onStart(Intent intent) {
        super.onStart(intent);
        super.setUIContent(ResourceTable.Layout_ability_main);

        btn1 = (Button) findComponentById(ResourceTable.Id_btn1);

        // 2.实现接口
        btn1.setClickedListener(this);

    }

    // 重写点击方法
    @Override
    public void onClick(Component component) {
        btn1.setText("被点了");
    }
    @Override
    public void onActive() {super.onActive();}

    @Override
    public void onForeground(Intent intent) {super.onForeground(intent);}

}
```

3. 方法引用

```java
public class MainAbilitySlice extends AbilitySlice implements Component.ClickedListener {

    Button btn1;
    @Override
    public void onStart(Intent intent) {
        super.onStart(intent);
        super.setUIContent(ResourceTable.Layout_ability_main);

        btn1 = (Button) findComponentById(ResourceTable.Id_btn1);

        // 3.方法引用
        btn1.setClickedListener(this::onClick);

    }

    @Override
    public void onClick(Component component) {
        btn1.setText("被点了");
    }

    @Override
    public void onActive() {
        super.onActive();
    }

    @Override
    public void onForeground(Intent intent) {
        super.onForeground(intent);
    }
}
```

4. 匿名内部类

```java
public class MainAbilitySlice extends AbilitySlice{

    Button btn1;
    @Override
    public void onStart(Intent intent) {
        super.onStart(intent);
        super.setUIContent(ResourceTable.Layout_ability_main);

        btn1 = (Button) findComponentById(ResourceTable.Id_btn1);

        // 4.匿名内部类
        btn1.setClickedListener(new Component.ClickedListener() {
            @Override
            public void onClick(Component component) {
                btn1.setText("被点了");
            }
        });

    }

    @Override
    public void onActive() {
        super.onActive();
    }

    @Override
    public void onForeground(Intent intent) {
        super.onForeground(intent);
    }
}
```

***

## 双击事件

- 接口名：DoubleClickedListener

```java
public class MainAbilitySlice extends AbilitySlice{

    Button btn1;
    @Override
    public void onStart(Intent intent) {
        super.onStart(intent);
        super.setUIContent(ResourceTable.Layout_ability_main);

        btn1 = (Button) findComponentById(ResourceTable.Id_btn1);

        // 绑定双击事件
        btn1.setDoubleClickedListener(new Component.DoubleClickedListener() {
            @Override
            public void onDoubleClick(Component component) {
                btn1.setText("被双击了");
            }
        });
    }

    @Override
    public void onActive() {
        super.onActive();
    }

    @Override
    public void onForeground(Intent intent) {
        super.onForeground(intent);
    }
}
```

***

## 长按事件

- 接口名：LongClickedListener

```java
public class MainAbilitySlice extends AbilitySlice{

    Button btn1;
    @Override
    public void onStart(Intent intent) {
        super.onStart(intent);
        super.setUIContent(ResourceTable.Layout_ability_main);

        btn1 = (Button) findComponentById(ResourceTable.Id_btn1);

        // 绑定长按事件
        btn1.setLongClickedListener(new Component.LongClickedListener() {
            @Override
            public void onLongClicked(Component component) {
                btn1.setText("被长按了");
            }
        });
    }

    @Override
    public void onActive() {
        super.onActive();
    }

    @Override
    public void onForeground(Intent intent) {
        super.onForeground(intent);
    }
}
```

***

## 滑动事件(触摸事件)

- 接口名：TouchEventListener

滑动事件里面分为三个动作：按下不松，移动，抬起。 

- PRIMARY_POINT_DOWN：按下不松。 
- POINT_MOVE：移动。 
- PRIMARY_POINT_UP：抬起。

>手机坐标： 手机左上角的点为原点。 （向右为X轴 | 向下为Y轴 | 垂直于屏幕向上为Z轴）

```java
import com.roydon.beautifyapp1.MainAbility;
import com.roydon.beautifyapp1.ResourceTable;
import ohos.aafwk.ability.AbilitySlice;
import ohos.aafwk.content.Intent;
import ohos.agp.components.Button;
import ohos.agp.components.Component;
import ohos.agp.components.DirectionalLayout;
import ohos.agp.window.dialog.ToastDialog;
import ohos.multimodalinput.event.MmiPoint;
import ohos.multimodalinput.event.TouchEvent;

public class MainAbilitySlice extends AbilitySlice{

    @Override
    public void onStart(Intent intent) {
        super.onStart(intent);
        super.setUIContent(ResourceTable.Layout_ability_main);

        DirectionalLayout dl = (DirectionalLayout) findComponentById(ResourceTable.Id_dl);

        dl.setTouchEventListener(new Component.TouchEventListener() {
            @Override
            public boolean onTouchEvent(Component component, TouchEvent touchEvent) {

                if (touchEvent.getAction()==TouchEvent.PRIMARY_POINT_DOWN){
                    System.out.println("按下");
                    //因为给布局 DirectionalLayout 绑定的触摸事件，所以可以获取手指在屏幕按下的位置
                    System.out.println("手指按下的坐标："+touchEvent.getPointerPosition(0));
                    MmiPoint position = touchEvent.getPointerPosition(0);
                    float pointX = position.getX();//按下点的横坐标
                    float pointY = position.getY();//按下点的纵坐标
                }else if(touchEvent.getAction()==TouchEvent.POINT_MOVE){
                    System.out.println("移动");
                    //移动时间同样有坐标方法，坐标随手指移动不断变化
                }else if(touchEvent.getAction()==TouchEvent.PRIMARY_POINT_UP){
                    System.out.println("松开");
                }

                return true;//若返回true继续事件，false反之
            }
        });

    }

    @Override
    public void onActive() {
        super.onActive();
    }

    @Override
    public void onForeground(Intent intent) {
        super.onForeground(intent);
    }
}
```

***

# 常见组件

屏幕展示出来的元素，都称之为组件。比如华为已经提供的：文本，图片，进度条，输入框等。 

组件的顶级父类：``Component``

## 组件分类

- 显示类组件 只负责数据展示的，无法跟用户交互，比如展示文本的组件，展示图片的组件。 
- 交互类组件 可以跟用户交互的，比如用户可以点击的按钮组件，用户可以输入的文本框组件。
-  布局类组件 布局其实也是一种比较特殊的组件。

## 显示类组件

文本Text、图片Image、CommonDialog普通弹框组件、ToastDialog信息提示组件、时钟Clock、定时器 TickTimer、进度条ProgressBar等。。。

### Text文本组件

- 作用：数据展示

常用属性：

![image-20220924174446530](C:\Users\31330\Pictures\Typora\image-20220924174446530.png)

长度单位：px，vp，fp。

如果不写单位，默认单位是px

vp（虚拟像素）长度单位。1vp=3px

fp字体大小单位。

跑马灯效果：



![](C:\Users\31330\Pictures\Typora\0000000000011111111.20220906142929.59811137630758749773991720039327.gif)

```java
// 跑马灯效果
text.setTruncationMode(Text.TruncationMode.AUTO_SCROLLING);
// 始终处于自动滚动状态
text.setAutoScrollingCount(Text.AUTO_SCROLLING_FOREVER);
// 启动跑马灯效果
text.startAutoScrolling();
```

***

### Image图片组件

- 作用：显示图片

图片存放路径再media文件夹下

![image-20220924175525053](C:\Users\31330\Pictures\Typora\image-20220924175525053.png)



图片剪切显示： 

- 代码中：可以用setClipGravity方法 
- xml文件中：可以用clip_alignment属性 
  - 上、下、左、右、居中 
  - 表示分别按照上、下、左、右、中间部位进行剪切。 

图片缩放显示： 

- 代码中：可以用setScaleMode方法 
- xml文件中：可以用scale_mode属性 
  - inside：表示将原图按比例缩放到与Image相同或更小的尺寸，并居中显示。 有可能不会填充组件 
  - center：表示不缩放，按Image大小显示原图中间部分。 
  - stretch：表示将原图缩放到与Image大小一致。 拉伸。将组件填充。
  - clip_center：表示将原图按比例缩放到与Image相同或更大的尺寸，并居中显示。超过组件的部分被剪 切掉。 
  - zoom_center：表示原图按照比例缩放到与Image最窄边一致，并居中显示。 
  - zoom_end：表示原图按照比例缩放到与Image最窄边一致，并靠结束端显示。 
  - zoom_start：表示原图按照比例缩放到与Image最窄边一致，并靠起始端显示。

***

### CommonDialog普通弹框组件

#### 使用默认布局的基本用法

```java
//把普通弹框弹出来就可以了
//1.创建弹框的对象
//this:当前弹框是哪展示在当前的界面中的。
CommonDialog cd = new CommonDialog(this);
//2.因为弹框里面是有默认布局的
//设置标题
cd.setTitleText("系统定位服务已关闭");
//设置内容
cd.setContentText("请打开定位服务，以便司机师傅能够准确接您上车");
//自动关闭
cd.setAutoClosable(true);
//设置按钮
//参数一：按钮的索引 0 1 2
//参数二：按钮上的文字
//参数三：点击了按钮之后能做什么
cd.setButton(0, "设置", new IDialog.ClickedListener() {
@Override
public void onClick(IDialog iDialog, int i) {
//写上点击了设置之后，要做的事情。
//如果点击之后我不需要做任何事情，在第三个参数中传递null就可以了。
}
});
cd.setButton(1, "取消", new IDialog.ClickedListener() {
@Override
public void onClick(IDialog iDialog, int i) {
//销毁弹框
cd.destroy();
}
});
//把弹框显示出来
cd.show();
}
```

#### 自定义弹框布局

新建弹窗布局文件，文件名： message_dialog.xml。如果需要更复杂的弹框，只要丰富xml文件中的组件即可。

```xml
<?xml version="1.0" encoding="utf-8"?>
<DirectionalLayout
    xmlns:ohos="http://schemas.huawei.com/res/ohos"
    ohos:height="match_content"
    ohos:width="match_content"
    ohos:orientation="vertical">

    <Text
        ohos:id="$+id:message"
        ohos:height="match_content"
        ohos:width="match_content"
        ohos:text_size="40fp"/>

    <Button
        ohos:id="$+id:submit"
        ohos:height="match_content"
        ohos:width="match_content"
        ohos:background_element="#21a896"
        ohos:text="确定"
        ohos:text_size="40fp"/>

    <Button
        ohos:id="$+id:cancel"
        ohos:height="match_content"
        ohos:width="match_content"
        ohos:background_element="#0021D9"
        ohos:text="取消"
        ohos:text_size="40fp"
        ohos:top_margin="10vp"
        />
</DirectionalLayout>
```

java类：

```java
import com.roydon.myapplication1.ResourceTable;
import ohos.aafwk.ability.AbilitySlice;
import ohos.aafwk.content.Intent;
import ohos.agp.components.*;
import ohos.agp.window.dialog.CommonDialog;

public class MainAbilitySlice extends AbilitySlice {
    @Override
    public void onStart(Intent intent) {
        super.onStart(intent);
        super.setUIContent(ResourceTable.Layout_ability_main);

        //创建一个弹框对象
        CommonDialog cd = new CommonDialog(this);
        cd.setCornerRadius(30);//设置弹窗圆角
        //把messagedislog的xml文件加载到内存当中。交给弹框并展示出来。
        //加载xml文件并获得一个布局对象
        //parse方法：加载一个xml文件，返回一个布局对象。
        //参数一：要加载的xml文件
        //参数二：该xml文件是否跟其他xml文件有关。如果无关是独立的，就写null就可以了
        //参数三：如果文件是独立的，那么直接写false
        DirectionalLayout dl = (DirectionalLayout) LayoutScatter.getInstance(this).parse(ResourceTable.Layout_message_dialog, null, false);

        Text title = (Text) dl.findComponentById(ResourceTable.Id_message);
        Button submit = (Button) dl.findComponentById(ResourceTable.Id_submit);
        Button cancel = (Button) dl.findComponentById(ResourceTable.Id_cancel);

        title.setText("msg");
        //给两个按钮添加单击事件
        submit.setClickedListener(new Component.ClickedListener() {
            @Override
            public void onClick(Component component) {
                title.setText("点击了确定按钮");
            }
        });
        cancel.setClickedListener(new Component.ClickedListener() {
            @Override
            public void onClick(Component component) {
                //当点击了取消按钮之后，把弹框给关闭
                cd.destroy();
            }
        });
        //此时布局对象跟弹框还没有任何关系.还需要把布局对象交给弹框才可以
        cd.setContentCustomComponent(dl);
        //让弹框展示出来
        cd.show();
    }

    @Override
    public void onActive() {
        super.onActive();
    }

    @Override
    public void onForeground(Intent intent) {
        super.onForeground(intent);
    }
}
```

封装成工具类

```java
import com.roydon.myapplication1.ResourceTable;
import ohos.agp.components.*;
import ohos.agp.window.dialog.CommonDialog;
import ohos.app.Context;

public class MyDialog {
    public static void showDialog(Context context, String msg) {
        CommonDialog cd = new CommonDialog(context);
        cd.setCornerRadius(30);
        DirectionalLayout dl = (DirectionalLayout) LayoutScatter.getInstance(context).parse(ResourceTable.Layout_message_dialog, null, false);
        Text title = (Text) dl.findComponentById(ResourceTable.Id_message);
        Button submit = (Button) dl.findComponentById(ResourceTable.Id_submit);
        Button cancel = (Button) dl.findComponentById(ResourceTable.Id_cancel);
        title.setText(msg);
        submit.setClickedListener(new Component.ClickedListener() {
            @Override
            public void onClick(Component component) {
                title.setText("点击了确定按钮");
            }
        });
        cancel.setClickedListener(new Component.ClickedListener() {
            @Override
            public void onClick(Component component) {
                cd.destroy();
            }
        });
        cd.setContentCustomComponent(dl);
        cd.show();
    }
}
```

***

### ToastDialog信息提示组件

也叫做吐司弹框。就是一个小提示而已。 ToastDialog是CommonDialog的子类，所以具备CommonDialog相关的特性。 也包含了标题，内容还有选择按钮。 一般来讲，吐司弹框我们只用中间的内容部分，因为他出现的意义就是为了提示信息的。

基本使用：

```java
ToastDialog t = new ToastDialog(this);
t.setText("要显示的内容")
t.setAlignment(LayoutAlignment.CENTER);
t.show();
```

相关设置：

```java
ToastDialog toastDialog = new ToastDialog(this);
//设置的大小。如果不写，默认包裹内容
toastDialog.setSize(DirectionalLayout.LayoutConfig.MATCH_CONTENT,
DirectionalLayout.LayoutConfig.MATCH_CONTENT);
//设置持续时间。如果不写，默认2秒
toastDialog.setDuration(2000);
//设置自动关闭。如果不写，就是自动关闭
toastDialog.setAutoClosable(true);
//设置位置。如果不写，默认居中
toastDialog.setAlignment(LayoutAlignment.CENTER);
//设置提示信息内容
toastDialog.setText("要显示的内容");
//让吐司展示出来
toastDialog.show();
```

自定义布局和抽取工具类：

布局xml文件命名为mytoast.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<DirectionalLayout
    xmlns:ohos="http://schemas.huawei.com/res/ohos"
    ohos:height="match_content"
    ohos:width="match_content"
    ohos:orientation="vertical">

    <Text
        ohos:id="$+id:msg"
        ohos:height="match_content"
        ohos:width="match_content"
        ohos:text_size="16fp"
        ohos:text_color="#FFFFFF"
        ohos:text_alignment="center"
        ohos:padding="20vp"
        ohos:margin="30vp"
        ohos:multiple_lines="true"
        ohos:background_element="#FF5B3535"/>

</DirectionalLayout>
```

工具类：

```java
import com.roydon.myapplication1.ResourceTable;
import ohos.agp.components.DirectionalLayout;
import ohos.agp.components.LayoutScatter;
import ohos.agp.utils.LayoutAlignment;
import ohos.agp.window.dialog.ToastDialog;
import ohos.app.Context;

public class MyToast {

    public static void showDialog(Context context, String msg) {
        //加载xml布局文件
        DirectionalLayout dl = (DirectionalLayout) LayoutScatter.getInstance(context).parse(ResourceTable.Layout_mytoast, null, false);
        ToastDialog td = new ToastDialog(context);
        td.setSize(DirectionalLayout.LayoutConfig.MATCH_CONTENT, DirectionalLayout.LayoutConfig.MATCH_CONTENT);
        td.setDuration(2000);//设置出现的时间
        td.setAutoClosable(true);//设置自动关闭
        td.setAlignment(LayoutAlignment.BOTTOM);//对其方式
        td.setText(msg);
        td.show();
    }
}
```

### Clock时钟组件

是Text的子类，所以可以使用Text的一些属性。

常用属性：

![image-20220924182911591](C:\Users\31330\Pictures\Typora\image-20220924182911591.png)

常用方法：

![image-20220924182926560](C:\Users\31330\Pictures\Typora\image-20220924182926560.png)

指定12小时展示格式 clock.setFormatIn12HourMode("yyyy年MM月dd日 hh:mm:ss a");

指定24小时展示格式 clock.setFormatIn24HourMode("yyyy年MM月dd日 HH:mm:ss");

拓展：

```java
//将字符串表示的时间（2021-01-01 11:11:11）转成毫秒值
public static String dateToTimeStamp(String s) throws ParseException{
	SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss"); 
	Date date = simpleDateFormat.parse(s); 
	long ts = date.getTime(); 
	String res = String.valueOf(ts); 
	return res;
}
//将时间的毫秒值转换为时间
public static String timeStampToDate(String s){
	SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss"); 
	long lt = new Long(s); 
	Date date = new Date(lt); 
	String res = simpleDateFormat.format(date);
	return res;
}
```

***

### TickTimer定时器组件

是Text的子类，所以可以使用Text的一些属性。

![image-20220924183532255](C:\Users\31330\Pictures\Typora\image-20220924183532255.png)

![image-20220924183540014](C:\Users\31330\Pictures\Typora\image-20220924183540014.png)

```xml
<TickTimer
	ohos:id="$+id:my_tt"
	ohos:height="60vp"
	ohos:width="250vp"
	ohos:padding="10vp"
	ohos:text_size="20fp"
	ohos:text_color="#ffffff"
	ohos:background_element="#0000ff"
	ohos:text_alignment="center"
	ohos:layout_alignment="horizontal_center"
	ohos:top_margin="50vp" />
	//没有设置时间，默认是从1970年1月1日开始。
```

***

### ProgressBar进度条组件

![image-20220924183828504](C:\Users\31330\Pictures\Typora\image-20220924183828504.png)

![image-20220924183839370](C:\Users\31330\Pictures\Typora\image-20220924183839370.png)

.getProgress();//获取进度条里面原本的值

.setProgressValue(progress);//设置进度值

.setProgressHintText(progress + "%");//修改提示文字进度

```xml
<ProgressBar
	ohos:id="$+id:pb"
	ohos:height="match_content"
	ohos:width="300vp"
	ohos:progress="0"
	ohos:progress_hint_text="0%"
	ohos:progress_hint_text_color="#000000"
	ohos:progress_width="50vp"
	ohos:progress_color="#FF0000"
	ohos:max="100"
	ohos:min="0"/>
```

***

### RoundProgressBar

是ProgressBar的子类，用法跟ProgressBar一模一样，只是显示的方式不一样。

```xml
<RoundProgressBar
	ohos:height="300vp"
	ohos:width="300vp"
	ohos:progress_hint_text="80%"
	ohos:progress_hint_text_size="50vp"
	ohos:progress_hint_text_color="#000000"
	ohos:progress="80"
	ohos:progress_width="20vp"
	ohos:progress_color="#FF0000"
	ohos:max="100"
	ohos:min="0"/>
```

***

## 交互类组件

### TextField文本输入框组件

是Text的子类，用来进行用户输入数据的。

![image-20220924184518703](C:\Users\31330\Pictures\Typora\image-20220924184518703.png)

将文本框中的密码变成明文：textField.setTextInputType(InputAttribute.PATTERN_NULL);

将文本框中的密码变回密文：textField.setTextInputType(InputAttribute.PATTERN_PASSWORD);

取消按钮设置位置：int x = r.nextInt(500); int y = r.nextInt(1000);cacel.setTranslation(x,y);

```xml
<TextField
	ohos:id="$+id:text"
	ohos:height="50vp"
	ohos:width="319vp"
	ohos:background_element="#FFFFFF"
	ohos:hint="请输入信息"
	ohos:hint_color="#999999"
	ohos:layout_alignment="horizontal_center"
	ohos:text_alignment="center"
	ohos:text_size="17fp"
	ohos:top_margin="100vp"/>
```

***

### Checkbox多选框组件

父类是AbsButton，而AbsButton的父类是Button。 当我们需要同时选择多个元素的时候就需要用到多选框组件。 

比如：发送图片的时候需要多选，注册的时候选择爱好也需要多选等。

![image-20220924185228886](C:\Users\31330\Pictures\Typora\image-20220924185228886.png)



![image-20220924185541682](C:\Users\31330\Pictures\Typora\image-20220924185541682.png)

可以给多选框添加一个状态监听事件 checkbox.setCheckedStateChangedListener(this);

```java
public class MainAbilitySlice extends AbilitySlice implements AbsButton.CheckedStateChangedListener
```

```java
//当多选框的状态被改变之后，就会调用这个方法
//参数一：absButton就表示状态被改变的那个多选框
//参数二：表示当前多选框的状态，true选中 false 未选中
@Override
public void onCheckedChanged(AbsButton absButton, boolean b) {
	if(b){
		ToastUtils.showDialog(this,"被选中");
	}else{
		ToastUtils.showDialog(this,"未被选中");
	}
}
```

***

### RadioButton单选框组件

父类是AbsButton，而AbsButton的父类是Button。在使用的时候需要用到单选按钮的按钮组。 RadioContainer，在一组内多选按钮只能选择其中一个。

当需要监听单选框的状态时，不要用AbsButton里面的CheckedStateChangedListener。而是给按钮组 RadioContainer添加事件。用RadioContainer里面的CheckedStateChangedListener。

按钮组RadioContainer常见方法：.setMarkChangedListener () //添加状态监听事件，可以监听按钮组里面单选按钮的状态是否改变

```java
public class MainAbilitySlice extends AbilitySlice implements RadioContainer.CheckedStateChangedListener
```

![image-20220924190522553](C:\Users\31330\Pictures\Typora\image-20220924190522553.png)

![image-20220924190530758](C:\Users\31330\Pictures\Typora\image-20220924190530758.png)



```xml
<RadioContainer
    ohos:id="$+id:rc"
    ohos:height="match_content"
    ohos:width="match_content">

    <RadioButton
        ohos:id="$+id:boy"
        ohos:height="match_content"
        ohos:width="match_content"
        ohos:background_element="#21a8fd"
        ohos:marked="false"
        ohos:text="男"
        ohos:text_alignment="center"
        ohos:text_size="30fp"
        />
    <RadioButton
        ohos:id="$+id:girl"
        ohos:height="match_content"
        ohos:width="match_content"
        ohos:background_element="#21a8fd"
        ohos:marked="false"
        ohos:text="女"
        ohos:text_alignment="center"
        ohos:text_size="30fp"
        ohos:top_margin="10vp"/>
</RadioContainer>
```

```java
RadioContainer rc = (RadioContainer) findComponentById(ResourceTable.Id_rc);
rc.setMarkChangedListener(this);
//当按钮组里面的按钮状态发生改变的时候，就会触发下面的方法
//参数一：单选框按钮组的对象
//参数二：索引，表示当前状态改变的是该按钮组中第几个按钮
@Override
public void onCheckedChanged(RadioContainer radioContainer, int i) {
	RadioButton rb = (RadioButton) radioContainer.getComponentAt(i);
	String text = rb.getText();
	if(rb.isChecked()){
		ToastUtils.showDialog(this,text + "被选中了");
	}else{
		ToastUtils.showDialog(this,text + "被取消选中了");
	}
}
```

***

### Switch组件

>滑道背景 ohos:track_element="#FF0000" 
>
>滑块颜色 ohos:thumb_element="#07C160"

![image-20220924192225391](C:\Users\31330\Pictures\Typora\image-20220924192225391.png)

```xml
<Switch
	ohos:id="$+id:choose"
	ohos:height="40vp"
	ohos:width="100vp"
	ohos:text_state_on="开"
	ohos:text_state_off="关"
	ohos:text_size="20vp"
	/>
```

监听状态改变：

```java
public class MainAbilitySlice extends AbilitySlice implements AbsButton.CheckedStateChangedListener
```

```java
Switch choose = (Switch) findComponentById(ResourceTable.Id_choose);
choose.setCheckedStateChangedListener(this);
//当开关组件状态发生改变的时候，那么就会调用这个方法
//参数一：表示状态改变的那个开关组件
//参数二：表示组件当前的状态
@Override
public void onCheckedChanged(AbsButton absButton, boolean b) {
	if(b){
		//ToastUtils.showDialog(this,"开关开启了");
		//可以打开某个设置
	}else{
		//ToastUtils.showDialog(this,"开关关闭了");
		//可以关闭某个设置
	}
}
```

***

### Slider滑块组件

```xml
<Slider
	ohos:height="50vp"
	ohos:width="300vp"
	进度颜色，左边的
	ohos:progress_color="#FF0000"
	滑块颜色
	ohos:thumb_element="#00FF00"
	未完成进度颜色
	ohos:background_instruct_element="#0000FF"
	次一级的进度值
	ohos:vice_progress="80"
	次一级的进度颜色
	ohos:vice_progress_element="#923456"
	是否允许用户操作滑块
	ohos:enabled="true"
	max = "100"
	min = "0"
	/>
```

![image-20220924192533960](C:\Users\31330\Pictures\Typora\image-20220924192533960.png)

事件：ValueChangedListener（值改变事件）

接口中的方法：

①：onProgressUpdated（参数一，参数二，参数三） 当滑块组件中的值改变的时候，调用该方法。 

>参数一：滑块对象 
>
>参数二：当前进度值 
>
>参数三：当前滑块组件是否可以调节进度

②：onTouchStart 按上滑块的时候触发 

③：onTouchend 离开滑块的时候触发

```java
public class MainAbilitySlice extends AbilitySlice implements Slider.ValueChangedListener
```

```java
Slider slider = (Slider) findComponentById(ResourceTable.Id_slider);
slider.setValueChangedListener(this);
//当滑块组件中的进度值改变的时候，就会调用这个方法
//参数一：滑块组件对象
//参数二：当前的进度值
//参数三：当前滑块是否可以被滑动
@Override
public void onProgressUpdated(Slider slider, int i, boolean b) {
	ToastUtils.showDialog(this,"当前的进度值为：" + i);
}
//当用户用鼠标或者用手指
//按下滑块不松的时候，会调用该方法
@Override
public void onTouchStart(Slider slider) {
	ToastUtils.showDialog(this,"按下不松");
}
//松开滑块的时候，会调用该方法。
@Override
public void onTouchEnd(Slider slider) {
	ToastUtils.showDialog(this,"松开");
}
```

***

### ListContainer

ListContainer是一个列表容器类组件。在这里的每一行，我们都可以看做是一个item。如下图所示，包裹了所有 item的红色的容器，就是ListContainer

> 注意细节： 
>
> ① 每一行其实就是一个独立的item。
>
>  ② 在屏幕的上面和下面，还有很多没有展示出来的item。 当我们用手指往上滑动的时候，就可以到下面的item。 当我们用手指往下滑动的时候，就可以到上面的item。 只不过划出屏幕的item会被销毁，而没有划入屏幕的item 还没有创建出来。 
>
> ③ 如果item过多，在内存会有垃圾。这个问题下面学习。

![image-20220924193634671](C:\Users\31330\Pictures\Typora\image-20220924193634671.png)

```xml
<ListContainer
	ohos:id="$+id:listcontainer"
	ohos:height="match_parent"
	ohos:width="match_parent"
	ohos:layout_alignment="horizontal_center"/>
```

实现步骤： 

1. 给item去指定一个布局xml文件 

```xml
<?xml version="1.0" encoding="utf-8"?>
<DirectionalLayout
	xmlns:ohos="http://schemas.huawei.com/res/ohos"
	ohos:height="match_content"
	ohos:width="match_content"
	ohos:orientation="horizontal">
	<Text
		ohos:id="$+id:text"
		ohos:height="match_content"
		ohos:width="match_content"
		ohos:text="00:00"
		ohos:text_size="20fp"/>
</DirectionalLayout>
```

2. 书写一个javabean类表示item 

```java
public class Item {
//记录的值就是赋值给item里面的text
	private String text;
	public Item() {}
	public Item(String text) {
		this.text = text;
	}
	public String getText() {
		return text;
	}
	public void setText(String text) {
		this.text = text;
	}
}
```

3. 写一个适配器类去管理item 

```java
import com.roydon.listcontainerdemo1.ResourceTable;
import com.roydon.listcontainerdemo1.bean.Item;
import ohos.aafwk.ability.AbilitySlice;
import ohos.agp.components.*;

import java.util.ArrayList;

public class ItemProvider extends BaseItemProvider {
    private ArrayList<Item> list;
    private AbilitySlice as;

    public ItemProvider(ArrayList<Item> list, AbilitySlice as) {
        this.list = list;
        this.as = as;
    }

    public ArrayList<Item> getList() {
        return list;
    }

    public void setList(ArrayList<Item> list) {
        this.list = list;
    }

    public AbilitySlice getAs() {
        return as;
    }

    public void setAs(AbilitySlice as) {
        this.as = as;
    }

    @Override
    public int getCount() {
        return list.size();
    }

    @Override
    public Object getItem(int i) {
        if (list != null && i >= 0 && i < list.size()) {
            return list.get(i);
        }
        return null;
    }

    @Override
    public long getItemId(int i) {
        return i;
    }

    @Override
    public Component getComponent(int i, Component component, ComponentContainer componentContainer) {
        DirectionalLayout dl;
        if (component != null) {
            // 优化
            dl = (DirectionalLayout) component;
        } else {
            dl = (DirectionalLayout) LayoutScatter.getInstance(as).parse(ResourceTable.Layout_list_item, null, false);
        }
        Text text = (Text) dl.findComponentById(ResourceTable.Id_text);
        text.setText(list.get(i).getText());
        return dl;
    }
}
```

4. 将适配器交给ListContainer

```java
import com.roydon.listcontainerdemo1.ResourceTable;
import com.roydon.listcontainerdemo1.bean.Item;
import com.roydon.listcontainerdemo1.provider.ItemProvider;
import ohos.aafwk.ability.AbilitySlice;
import ohos.aafwk.content.Intent;
import ohos.agp.components.ListContainer;

import java.util.ArrayList;

public class MainAbilitySlice extends AbilitySlice {
    @Override
    public void onStart(Intent intent) {
        super.onStart(intent);
        super.setUIContent(ResourceTable.Layout_ability_main);

        ListContainer listContainer = (ListContainer) findComponentById(ResourceTable.Id_listContainer);

        //1.数据传给item视图
        ItemProvider itemProvider = new ItemProvider(getData(), this);
        //2.item视图传到ListContainer
        listContainer.setItemProvider(itemProvider);

    }

    @Override
    public void onActive() {
        super.onActive();
    }

    @Override
    public void onForeground(Intent intent) {
        super.onForeground(intent);
    }

    public ArrayList<Item> getData() {
        ArrayList<Item> list = new ArrayList<>();
        for (int i = 0; i < 50; i++) {
            list.add(new Item("item-->" + i));
        }
        return list;
    }

}
```

***

案例：微信消息

### Picker

picker是滑动选择器组件。在一些app中选择地址的时候会用到，但是一般是三个picker选择器组合在一起使用。 如图所示：

![image-20220924202616824](C:\Users\31330\Pictures\Typora\image-20220924202616824.png)

案例：选择今天星期几

```xml
<Picker
        ohos:id="$+id:picker"
        ohos:height="match_content"
        ohos:width="100vp"
        ohos:max_value="6"
        ohos:min_value="0"
        ohos:normal_text_color="#21a8fd"
        ohos:normal_text_size="20fp"
        ohos:selected_text_color="#FF0000"
        ohos:selected_text_size="20fp"
        ohos:shader_color="pink"
        ohos:value="0"
        />
```

```java
Picker picker = (Picker) findComponentById(ResourceTable.Id_picker);
//把要展示的内容全部放在集合中
ArrayList<String> list = new ArrayList<>();
list.add("星期一");
list.add("星期二");
list.add("星期三");
list.add("星期四");
list.add("星期五");
list.add("星期六");
list.add("星期日");
//设置内容
picker.setFormatter(list::get)
```

Picker联动时

```java
public class MainAbilitySlice extends AbilitySlice implements Picker.ValueChangedListener
```

```java
//参数一：表示当前数据变动的那个滑动选择器对象
//参数二：表示旧值 (原来选中的值)
//参数三：表示新值（现在选中的值）
@Override
public void onValueChanged(Picker picker, int oldValue, int newValue) {
    if (picker == province) {
     	Province chooseProvince = provinceList.get(newValue);//获取当前省份
        
        city.setMaxValue(chooseProvince.getList().size() - 1);
        city.setFormatter(i -> chooseProvince.getList().get(i));
        city.setValue(0);//当前面更换省份的时候，中间的城市需要从第一个开始展示
    }
}
```

案例：省市区三级联动

***

### DatePicker和TimePicker

 DatePicker和TimePicker都是时间选择器。

> DatePicker：表示年月日 
>
> TimePicker：表示时分秒

```xml
<DatePicker
	ohos:id="$+id:datepicker"
	ohos:height="match_content"
	ohos:width="300vp"
	ohos:normal_text_size="20fp"
	ohos:selected_text_size="20fp"/>
<TimePicker
	ohos:id="$+id:timepicker"
	ohos:height="match_content"
	ohos:width="300vp"
	ohos:normal_text_size="20fp"
	ohos:selected_text_size="20fp"/>
```

DatePicker监听：

```java
public class MainAbilitySlice extends AbilitySlice implements DatePicker.ValueChangedListener
```

```java
DatePicker datePicker = (DatePicker) findComponentById(ResourceTable.Id_datepicker);
datePicker.setValueChangedListener(this);
@Override
public void onValueChanged(DatePicker datePicker, int year, int month, int day) {
	text.setText(year + "年" + month + "月" + day + "日");
}
```

TimePicker监听：

```java
TimePicker timePicker = (TimePicker) findComponentById(ResourceTable.Id_timepicker);
timePicker.setTimeChangedListener(new TimePicker.TimeChangedListener() {
	@Override
	public void onTimeChanged(TimePicker timePicker, int hour, int minutes, int second) {
		text.setText("时间为:" + hour + minutes + second);
	}
});
```

***

# 美化组件



- 美化外形 

  - 组件外形（方形，圆角，胶囊形，圆形）
  - 组件边框（颜色，粗细） 背景颜色（有色号就行）
  - 背景渐变（线形或者辐射形） 

- 美化状态 

  组件在不同状态时显示不同的样式。 

  暂时掌握三中状态： 

  - 默认状态 （所有组件都有默认状态）
  - 按下状态 （组件按下不松时的状态） 
  - 选中状态 （开关组件，多选按钮，单选按钮的开启状态）



## shape标签

在graphic包中新建xml，根标签为：shape就可以自定义组件的形状。

根标签：shape

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<shape xmlns:ohos="http://schemas.huawei.com/res/ohos"
       ohos:shape="rectangle">
    <solid
        ohos:color="#FFFFFF"/>
    <corners
        ohos:radius="15vp"/>
</shape>
```

> 根标签包含一个属性：shape --> ohos:shape="rectangle"
>
> 常用值： 1. rectangle：长方形 2. oval：椭圆 

> 根标签包含五个子标签：
>
> ① stroke：绘制边框 
>
> - 属性： 
>   - 宽度，颜色 
>
> ② corners：圆角 
>
> - 属性： 
>
>   - radius半径 (主要)
>
>   - left_top_x、left_top_y 左上
>
>   - right_top_x、right_top_y 右上 
>   - left_bottom_x、left_bottom_y 左下 
>   - right_bottom_x、right_bottom_y 右下 
>
> ③ solid：背景填充 
>
> - 属性： 
>   - color 只能指定一个颜色 
>   - colors 可以指定多个颜色，渐变。 
>
> ④ bounds：边框 可以单独设置上下左右的边框。 
>
> ⑤ gradient：渐变 
>
> - 属性： 
>   - shader_type：类型 --- radial（辐射） linear（线性）

***

## state-container标签

在graphic包中新建xml，根标签为：state-container ，就可以在不同状态下美化组件

```xml
<?xml version="1.0" encoding="utf-8"?>
<state-container
    xmlns:ohos="http://schemas.huawei.com/res/ohos">

    /按下
    <item ohos:state="component_state_pressed" ohos:element="#000000"/>
    //打开状态
    <item ohos:state="component_state_checked" ohos:element="#FF0000"/>
    //默认状态：要写在最下面
    <item ohos:state="component_state_empty" ohos:element="#21a8f6"/>

</state-container>
```

- 默认状态： component_state_empty （必须要写在最下面）
- 按下不松的状态： component_state_pressed 
- 打开状态： component_state_checked

> element中可以写指定的色号，也可以指定根标签为shape的xml文件，也可以指定固定的图片。



