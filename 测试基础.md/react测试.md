# React 测试
笔记,随记  

const wrapper = shallow(组件)  
shallow 单元测试一个组件。不会去测试组件下子组件的行为  

const wrapper = mount(组件)  
mount 测试 穿过 组件一整个生命周期  

- toBe 
```
expect('AAA').toBe('AAA')   => 比对字符串  
```


- toHaveLength  
```
expect([1,2,3]).toHaveLength(3);  =>  断言长度(数组)  
expect('123').toHaveLength(3);  =>  断言长度(字符串)  
expect('123').not.toHaveLength(2);  =>  断言长度(字符串)(非)  
```


- toEqual 断言等于    
- wrapper.type() 返回节点的类型(如果是DOM原生节点，返回string类型)  
```
const wrapper = mount(<div/>)  
expect(wrapper.type()).to.equal('div')  

const wrapper = mount(<Foo/>)  
expect(wrapper.type()).to.equal(Foo)  
```


- at(index)  返回 wrapper包装的节点的 索引  
```
  const wrapper = mount(<MyComponent/>);
  expect(wrapper.at(0).props('prefixCls')).toBe('aaa')
```


- find('div') 查找符合条件的 每一个节点  

```
const wrapper = mount(<MyComponent/>)
expect(wrapper.find('.foo')).to.have.length(1);
```


- setProps 设置一个属性或方法的默认值,react中触发 componentWillReceiveProps()  
```
wrapper.setProps({ type:'textarea' })
expect(wrapper.at(0).prop('type')).toBe('textarea');
```


- simulate 模拟一个动作  触发相应的方法 例如: click
```
let input = wrapper.find('foo').at(0);
input.simulate('click')
```

- toMatchSnapshot : jest中的toMatchSnapshot api判断两个条件一致与否。  
  原来要写成 expect(store.getActions()).toEqual({data...});这样，你需要把equal 里的东西都得具体描写清楚。  
  而 toMatchSnapshot可在当前目录下生成一个snapshot存放这个当前结果，写测试时一眼结果是预期的就可以commit.  
  如果改坏了函数就不匹配snapshot了.  
启动测试  会生成一个(__snapshots__)快照文件  