cocos2dx������3.x�Ժ�������Ŀ�ṹ�����ܶ࣬���˾��øĵúܲ���ģ�����Ŀ������˵����Ҫ�м��㣺

1������Ҫ����libcocos2dx��lib��Ŀ�ˣ��ܶ��Ŷ���cocos2dx����������Ŀ��ǣ�������cocos2dx�汾��ʱ���������Ŀ�ͺ����ڣ���3.x�£�������srcĿ¼�����������⡣

2���������еľ�̬�ⶼǿ���������ӣ�һ���̶��ϻ��СĿ�����

3���󲿷ֵط����������Ŀ¼��2.x�ºܶණ����������һЩȫ�ֺ꣬�ڴ����汾ʱҲ�ǳ�ʹ�ࡣ

4����cocos�������ŵ���Ŀ�����ˣ���ʵ���Ǻܶ���Ŀ�����������ģ�����������Ŀ�������һ��Ҳ��Ϊ����Ŀ����ʱ��������Ϊĳ����Ŀ���������Ӱ����������Ŀ������cocos���߸��ƴ����������̫ʹ���ˣ���ʵ�����ȫ������Ŀ��������......����Ҳ�����ܽ����ˣ����ƴ���ĺô�Ҳ���еģ�������ĿĿ¼�ṹ����ȷ�������ܶ���Ҳ����ܶࡣ

���ڻ�����һЩ�Ŷӻ�ʹ��2.x�İ汾����ʵ2.x����Ŀ����һ�£�����3.x��һЩ���Ի��Ǻ����׵ģ�����ʹ�ŵ���һ�£�

1�������Զ����ɵ���Ŀ��ADT���档

2������������ṩ��src����������ǣ�

ADT��`�һ�������->Properties->Java Build Path->Source->Link Source->Browse`��

�ҵ�Cocos2d-x�����Ŀ¼��`cocos/platform/android/java/src`�����룬���ָ�libcocos2dx�����finish��OK��

3�������windows�£���NDK���룬��Ҫ��Build command����������ǣ�`ADT���һ�������->Properties->C/C++ Build->Builder Settings->Build command`����NDKĿ¼�µ�ndk-build.cmd���ɣ�

`${NDK_ROOT}/ndk-build.cmd`

4���ҵ� jni����� Android.mk�ļ������ӱ�����ĿĿ¼��
```make
$(call import-add-path,$(LOCAL_PATH)/../../../../)

include $(BUILD_SHARED_LIBRARY)[/code]
```
5����̬�ⲻǿ��ȫ�����ӣ������޸� Android.mk �ļ����� `LOCAL_WHOLE_STATIC_LIBRARIES` �ĳ� `LOCAL_STATIC_LIBRARIES`�����Ǽ�ס��**���������һЩ�����⣬�����������б���Ҫ������Native���룬Ʃ���java���õ�JNI���룬�Ͳ�����������**��

ʵ�ʲ������������������Ժ��С����С�Ƚ�����*��������Ŀ��.so�ļ���ż�С��10%-20%��*��cocos2dx 2.x�汾������϶Ȼ���̫���ˣ�Ҫ����ھ���С�

6������Ŀ����� Classes��cocos2dx��extensions����Ŀ¼ɾ���ɣ��Լ����һ�£�

`C/C++ General -> Paths and Symbols -> Source Location -> Link Folder`

Folder name �� classes��Link to folder in the file system���ϣ�����Ŀ�� classes ����·�����ϡ�

7����Ŀǰ��cocos2dx�������������android sdk�İ汾��װһ�£�8��18����ֻ��Ҫװ SDK Platform���ɡ�

8�������ڵ�2�����棬���ǰ�libcocos2dxֱ�Ӽӵ���Ŀ�����ˣ����Կ��Ե���Ŀ�������棬��libcocos2dx��Libraryɾ���ˣ������Ŀ���ڻ��������ж��cocos2dx�汾������˵��ʹ���ˣ�ֱ�Ӽӵ�������������ʡ�µ�������

`Properties -> Android`

**ע�⣺�������е�library��Ŀ���������ģ�ֻ�д��������Ŀ����������Ŷ��**

9��c++���������Eclipse��򿪣����ǻᱨһ�Ѵ��ҿ�pathʲô�Ķ������õĶԵģ���ʱû�ر�õĽ���������򵥵�Ĵ�����ǰ�c/c++�Ĵ�������ص���

`Properties -> C/C++ General -> Code Analysis`

ѡ�� `Use project settings`��Ȼ��������ȫ����ѡ�򶼹��ϡ�

���軹���е��ģ������������ǵ�[heysdktools](https://github.com/heysdk/heysdktools)���߰���ִ�� `proccc2proj.cmd` ���� `proccc2proj.sh` ����һ���㶨��Ŀ��