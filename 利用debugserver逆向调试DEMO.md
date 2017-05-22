##利用lldb配合debugserver逆向调试DEMO



###代码

```
- (void)viewDidLoad {
    [super viewDidLoad];
    UIButton *button  = [UIButton buttonWithType:UIButtonTypeSystem];
    button.backgroundColor = [UIColor grayColor];
    [button setTitle:@"点我" forState:UIControlStateNormal];
    [button setTitleColor:[UIColor redColor] forState:UIControlStateNormal];
    button.frame = CGRectMake(50, 200, 100, 60);
    [button addTarget:self action:@selector(buttonClock:) forControlEvents:UIControlEventTouchUpInside];
    [self.view addSubview:button];
}

- (void)buttonClock:(UIButton *)button
{
    Animal *dog = [[Animal alloc] init];
    [dog speak:^(NSString *name, NSString *content) {
        NSLog(@"%@:%@",name, content);
    }];
}

```

###调试前预备
- 将demo运行到设备上
- debugserver在`/usr/bin/debugserver_arm64`路径下
- 用debugserver启动或者附加进程
	- 使用`ps -ef`找到demo APP的二进制文件所在路径

###debugserver附加进程
```
umiumi:~ root# debugserver_arm64 -x  backboard *:1234 /var/mobile/Containers/Bundle/Application/F64AA674-8595-4883-8491-DA262684B008/iOSRE_block.app/iOSRE_block 
debugserver-@(#)PROGRAM:debugserver  PROJECT:debugserver-320.2.89
 for arm64.
Listening to port 1234 for a connection from *...
```