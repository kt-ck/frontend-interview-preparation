# React

1. 生命周期：

   1. 初始化阶段：constructor中对state、props进行赋值，并且不会调用update

   2. 挂载阶段

      render

      componentDidMount

   3. 更新阶段

      1. 由props的更新引起的操作

         1. componentWillReceiveProps(nextProps, nextState)

            可以对state进行设置，合并state

         2. shouldComponentUpdate(nextProps,nextState)

            返回boolean类型数据。如果返回false，就不继续执行生命周期函数了，不能设置state

         3. render

         4. componentDidUpdate(prevProps, prevState)

      2. 由state更新引起的操作

         1. shouldComponentUpdate
         2. render
         3. ComponentDidUpdate

   4. 卸载阶段:componentWillUnmount

      

2. refs

   1. 什么时候使用？
      1. 管理焦点，文本选择或者媒体播放
      2. 触发强制动画
      3. 集成第三方库

   2. 在class中使用refs

      ```react
      //1. 创建refs this.refs = createRef();
      //2. 在需要引用的html标签或者是对象上加上ref={this.refs}
      //3. 可以通过this.refs.current引用到对象了
      ```

   3. refs转发

      ```react
      const Button = React.forwardRef((props, ref)=>{
          <button ref={ref}>
          	props.children
          </button>
      });
      
      const ref = React.createRef();
      <Button ref={ref}>click me</Button>
      ```

3. fragment

   ```react
   render(){
       return (
       	<React.Fragment key={}>
            
           </React.Fragment>
           
           //或者
           <>
           <td></td>
           <td></td>
           </>
       )
   }
   
   
   ```

   

