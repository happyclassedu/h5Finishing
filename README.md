# H5--移动端知识点整理 <br/>
## 1. 在UC浏览器下input光标定位的问题。<br/>
  ### 比如如下简单的代码，给input框设置高度和行高；<br/>
  ### 如下代码：<br/>
  <input type="text" class="input-cls"/>
  <pre>
  a,button,input,optgroup,select,textarea{
    outline: none;
  }
  .input-cls {
    width:10rem;
    height:2rem;
    border:1px solid red;
    line-height: 2rem;
    text-indent: 0.12rem;
    font-size: 1rem;
  }
  </pre>
  在UC浏览器下会显示如下效果: <br/>
  <img src="http://images2015.cnblogs.com/blog/561794/201606/561794-20160625170655344-1968154825.jpg"/><br/>
  其他浏览器下还好，但是比如qq浏览器一刚开始光标在整个input框内，当输入的时候，会居中对齐；<br/>
  ## 如上解决的方法有2种；<br/>
  ## 第一种方案是不设置input的行高；如下代码：<br/>
  <pre>
    .input-cls {
      width:10rem;
      height:2rem;
      border:1px solid red;
      text-indent: 0.12rem;
      font-size: 1rem;
    }
  </pre><br/>

  ## 第二种解决方法是设置padding和高度一起使用；<br/>
  代码如下：
  <pre>
    .input-cls {
      width:10rem;
      height:1rem;
      line-height:1rem;
      padding:0.5rem 0;
      border:1px solid red;
      text-indent: 0.12rem;
      font-size: 1rem;
    }
  </pre><br/>
 在UC浏览器下会显示如下效果: <br/>
  <img src="http://images2015.cnblogs.com/blog/561794/201606/561794-20160625170720844-987241925.jpg"/>
  <br/>
## 2. 去除手机浏览器input焦点的默认边框；比如如下这样的：<br/>
   <img src="http://images2015.cnblogs.com/blog/561794/201606/561794-20160625175059906-1845942393.png"/> <br/>
   解决的方法，在css加如下代码即可：
   <pre>
    a,button,input,optgroup,select,textarea{
      outline: none;
    }
   </pre>

## 3. 解决IOS下底部定位fixed的bug问题；
      很多资料说 "iOS下的 Fixed + Input 调用键盘的时候fixed无效问题" 可以使用如下方法可以解决；
      或者说其他地方也可以使用该方法，比如底部固定，顶部也使用fixed固定，中间内容有很多的情况下，可以鼠标进行滑动操作，
      或者更具体说需要使用滚动条，在内部滑动，且在IOS下更轻松滑动；可以使用如下方法解决；
      HTMl代码如下：
      <header class="head">顶部固定区域</header>
       <div class="content">
         <p>很多p标签内容</p>
       </div>
       <footer class="foot">
         底部
       </footer>
       CSS代码如下：
       <pre>
          <style>
            header, footer, main {
              display: block;
            }
            header {
              position: fixed;
              left: 0;
              top: 0;
              width:100%;
              height: 50px;
              background-color: red;
            }
            footer {
              position: fixed;
              left: 0;
              bottom: 0;
              background: red;
              width:100%;
              height: 50px; 
            }
            .content{
              /* 绝对定位，进行内部滚动 */
              position: absolute;
              top:50px;
              bottom: 50px;
              width: 100%;
              /* 使之可以滚动 */
              overflow-y: scroll;

              /* 增加该属性，可以增加弹性，是滑动更加顺畅 */
              -webkit-overflow-scrolling: touch;
              overflow-scrolling: touch;
            }
            .content p {
              width:100%;
            }
         </style>
       </pre>
## 4. Reactjs在ios设备上onClick事件失效的解决办法
      比如在react中一个div绑定事件，点击它，在IOS下会点击不了，但是在安卓下或者浏览器下都是正常的；比如如下React
      代码：
      <pre>
        var testDiv = React.createClass({
          fn : function(){
              alert('component was clicked!');
          },
          render:function(){
              return (
                  <div className="clickme" onClick={me.renderData}></div>
              )
          }
        });
      </pre>
  解决的办法有如下几种：
  1. 把div标签改成input标签，然后设置input的type为button，或者改为a标签就可以解决；
  2. 第二种方法是给div标签加一个样式，设置div{cursor:pointer;} 也可以解决，但是这种方案在编写css的
     时候最好注释一下，因为如果不注释的话，很有可能时间长了或者重构代码的时候，会忽略掉这种情况，导致以后
     会出现bug的可能；
  3. 在组件中的componentDidMount方法中，为该div绑定事件，在回调函数中写入想要实现的逻辑。