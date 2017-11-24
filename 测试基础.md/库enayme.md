#  enayme 库 使用

-[render](#render)  
-[shallow](#shallow)  


### render

Static Rendering API  
渲染react组件 为 html静态文件并且处理相应业务逻辑  

```
  const data = [{
    key: '1',
    firstName: 'John',
    lastName: 'Brown',
    age: 32,
  }, {
    key: '2',
    firstName: 'Jim',
    lastName: 'Green',
    age: 42,
  }];

  const wrapper = render(
    <Table dataSource={data} pagination={false}>
      <Button></Button>
    </Table>
  );

  expect(wrapper).toMatchSnapshot();
```


### shallow

创建表层组件  

```
   const wrapper = shallow(<Table columns={columns} />);

   const newColumns = [{
      title: 'Title',
      key: 'title',
      dataIndex: 'title',
    }];
  wrapper.setProps({ columns: newColumns });
  expect(wrapper.instance().columns).toBe(newColumns);
```


### mount

创建深层组件(可处理props等)

```
  const wrapper = mount(<Table loading={loading} />);
  expect(wrapper.find('.w-table')).toHaveLength(1);
```
