# rtmpdemo（Android）

1、下载rtmpdemo到本地

2、将rtmpdemo里面的android/app/libs/LiteAVSDK_Smart_8.1.9717.arr复制一份到自己自己的libs文件夹里

3、在android/build.gradle添加如下代码

 allprojects {
        flatDir{
            dirs 'libs'
        }
        }


4、在android/app/build.gradle下的两个地方添加如下代码

一、  defaultConfig{
         
          ndk {//
                    abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
                }
          javaCompileOptions { annotationProcessorOptions { includeCompileClasspath = true } }
      }
      
二、  dependencies {

      ...
      implementation(name: 'LiteAVSDK_Smart_8.1.9717', ext: 'aar')//

      }
      
5、把rtmpdemo下的android/app/src/main/java/com/rtmpdemo/view的整个view文件夹放到自己项目同一路径下
      
      
6、在 MainApplication.java把包名引入

import com.rtmpdemo.view.AppReactPackage;  


packages.add(new AppReactPackage());  //添加在return packages;前


7、前端页面的调用
一、复制rtmpdemo/app/TXCloudVideoView.js粘贴到自己公用组件里，这个就是将要调用的直播组件



二、使用 url改为自己需要的链接


// /*
// *设备管理
// * */
import React, {Component} from 'react';
import {
    View,
    Text,
    StyleSheet,
    Image,
    TouchableOpacity,
    NativeModules,
    NativeEventEmitter,
    DeviceEventEmitter, ScrollView,
} from 'react-native'
import TXCloudVedioView from './TXCloudVideoView';

export default class deviceManager extends Component{
    constructor(props,context) {
      super(props, context);

      };

    componentDidMount() {
    DeviceEventEmitter.addListener('startPlay', () => {
        console.warn("startPlay--》");

    });
    }


    render(){
        return(
            <View style={{flex:1,backgroundColor:"#fff"}}>
                <TXCloudVedioView
                    style={{width: '100%', height: 200}}
                    url={'rtmp://192.168.0.253:2022/live'}/>    
            </View>
        )
    }
}














