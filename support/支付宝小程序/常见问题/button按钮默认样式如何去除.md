在小程序当前页面的 page.acss 里添加样式清除或者在 app.acss 里添加，参考以下代码。<br />**注意：** 在 app.acss 里添加，所有 button 都会改。
```css
button { 
  background-color: transparent; 
  padding: 0; 
  margin: 0; 
  position: static;
  border: 0;
  border-radius: 0; 
  color: transparent;
}
button::after {  
  content: ''; 
  width: 0;
  height: 0;
  -webkit-transform: scale(1);
  transform: scale(1);  
  display: none;  
  background: transparent;
}
```
