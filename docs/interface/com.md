---
title: 用作 COM 组件
author: 夜輪風超絶技巧変奏曲
category: interface
layout: post
---
原文：[CeVIO AI ユーザーズガイド ┃ COMコンポーネントとして利用](https://cevio.jp/guide/cevio_ai/interface/com/)

---
C++ 和 VBScript 等程序的接口。

可以使用专用 API 精细地控制情绪、状态等。

## API 规范

```cpp
// 提供读说功能。
interface ITalker2V40
{
    uint Volume { get; set; }
    // 获取或设置音量（0～100）。

    uint Speed { get; set; }
    // 获取或设置语速（0～100）。

    uint Tone { get; set; }
    // 获取或设置音高（0～100）。

    uint ToneScale { get; set; }
    // 获取或设置音调（0～100）。

    uint Alpha { get; set; }
    // 获取或设置音色（0～100）。

    ITalkerComponentArray2 Components { get; }
    // 获取当前角色的情绪参数。
    // 备注：
    // 　内容会随着角色变化。
    // 　例1『さとうささら』→ "普通", "元気", "怒り", "哀しみ"
    // 　例2『小春六花』→ "嬉しい", "普通", "怒り", "哀しみ", "落ち着き"
    // 注意：
    // 　在 Visual C++ 环境中使用智能指针时，该类型被替换为以下类型。
    // 　ITalkerComponentArray2Ptr

    string Cast { get; set; }
    // 获取或设置角色。

    IStringArray AvailableCasts { get; }
    // 获取可以使用的角色名。
    // 备注：
    // 　能获取到的角色取决于已安装的音源。
    // 注意：
    // 　在 Visual C++ 环境中使用智能指针时，该类型被替换为以下类型。
    // 　IStringArray2Ptr

    ISpeakingState2 Speak(string text);
    // 开始播放指定的台词。
    // 参数：
    // 　text - 台词。
    // 返回值：
    // 　表示播放状态的对象。
    // 备注：
    // 　该函数返回而不等待播放结束。
    // 　要等待播放结束，请调用返回值 (ISpeakingState2) 的 Wait。
    // 注意：
    // 　在 Visual C++ 环境中使用智能指针时，该类型被替换为以下类型。
    // 　ISpeakingState2Ptr

    bool Stop();
    // 停止播放。
    // 返回值：
    // 　成功时返回true。其他情况返回false。

    double GetTextDuration(string text);
    // 获取指定台词的长度。
    // 参数：
    // 　text - 台词。
    // 返回值：
    // 　长度。单位是秒。

    IPhonemeDataArray2 GetPhonemes(string text);
    // 获取指定台词的音素单位的数据。
    // 参数：
    // 　text - 台词。
    // 返回值：
    // 　音素单位的数据。
    // 备注：
    // 　可以用于对口型。
    // 注意：
    // 　在 Visual C++ 环境中使用智能指针时，该类型被替换为以下类型。
    // 　IPhonemeDataArray2Ptr

    bool OutputWaveToFile(string text, string path);
    // 将指定台词输出为 WAV 文件。
    // 参数：
    // 　text - 台词。
    // 　path - 输出路径。
    // 返回值：
    // 　成功时返回true。其他情况返回false。
    // 备注：
    // 　输出格式为采样率 48kHz，比特率 16bit，单声道。
}

// 表示角色的情绪参数图的对象。
interface ITalkerComponentArray2
{
    int Length { get; }
    // 获取元素的数量。

    ITalkerComponent2 At(int index) { get; }
    // 获取具有指定索引的元素。
    // 参数：
    // 　index - 索引。
    // 返回值：
    // 　元素。

    ITalkerComponent2 ByName(string name) { get; }
    // 获取具有指定名称的元素。
    // 参数：
    // 　name - 名字。
    // 返回值：
    // 　元素。

    ITalkerComponentArray2 Duplicate();
    // 复制数组。
    // 返回值：
    // 　复制完毕的数组的索引。
}

// 情绪参数的单位对象。
interface ITalkerComponent2
{
    string Id { get; }
    // 获取标识符。

    string Name { get; }
    // 获取情绪的名字。（文本编码为Unicode）

    uint Value { get; set; }
    // 获取或设置情绪的值（0～100）。
}

// 表示播放状态的对象。
interface ISpeakingState2
{
    bool IsCompleted { get; }
    // 获取播放的状态（是否完成）。
    // 完成的情况返回true。（包括失败在内）其他情况返回false。

    bool IsSucceeded { get; }
    // 获取播放的状态（是否成功）。
    // 成功时返回true。其他情况返回false。

    void Wait();
    // 等待播放结束。

    void Wait_2(double timeout);
    // 等待播放结束。
    // 参数：
    // 　timeout - 最大等待时间。单位是秒。（0以下为无限）
}

// 表示音素数据数组的对象。
interface IPhonemeDataArray2
{
    int Length { get; }
    // 获取元素的数量。

    IPhonemeData2 At(int index);
    // 获取具有指定索引的元素。
    // 参数：
    // 　index - 索引。
    // 返回值：
    // 　元素。

    IPhonemeDataArray2 Duplicate();
    // 复制数组。
    // 返回值：
    // 　复制完毕的数组的索引。
}

// 表示音素数据单位的对象。
interface IPhonemeData2
{
    string Phoneme { get; }
    // 获取音素。

    double StartTime { get; }
    // 获取开始时间。单位是秒。

    double EndTime { get; }
    // 获取结束时间。单位是秒。
}

// 表示字符串数组的对象。
interface IStringArray2
{
    int Length { get; }
    // 获取元素的数量。

    string At(int index);
    // 获取具有指定索引的元素。
    // 参数：
    // 　index - 索引。
    // 返回值：
    // 　元素。

    IStringArray2 Duplicate();
    // 复制数组。
    // 返回值：
    // 　复制完毕的数组的索引。
}

// 提供【CeVIO AI】的控制功能。
interface IServiceControl2V40
{
    string HostVersion { get; }
    // 获取【CeVIO Creative Studio】(1)的客户端版本。

    string InterfaceVersion { get; }
    // 获取该接口的版本。

    static bool IsHostStarted { get; }
    // 获取【CeVIO Creative Studio】的可访问情况。

    int StartHost(bool noWait);
    // 启动【CeVIO Creative Studio】。如果已启动则无效。
    // 参数：
    // 　noWait - true时仅启动。关于可访问情况，可以通过 IsHostStarted 确认。
    // 　　　　　　false时不会返回控制，直到启动后允许外部访问后。
    // 返回值：
    // 　 0：成功。包括已启动的情况。
    // 　-1：无法确认安装状态。
    // 　-2：找不到可执行文件。
    // 　-3：无法启动进程。
    // 　-4：应用程序在启动后因错误而终止。

    void CloseHost(int mode);
    // 请求退出【CeVIO Creative Studio】。
    // 参数：
    // 　mode - 处理模式。
    // 　 0：如果【CeVIO AI】正在编辑，可以保存，取消退出等。
}
```

1. 原文如此。下同。

## 示例项目

=== "C++"

    ```cpp
    // 导入类型库
    // ※安装【CeVIO AI】时会注册该类型库
    #import "libid:7E3B8901-0A65-44A0-9A9A-5F9F822D0716" 
        named_guids rename_namespace("CeVIO")

    int main()
    {
        // COM初始化
        ::CoInitialize(NULL);

        // 生成ServiceControl实例
        CeVIO::IServiceControl2V40* pServiceControl;
        HRESULT result0 = ::CoCreateInstance(CeVIO::CLSID_ServiceControl2V40,
            NULL,
            CLSCTX_INPROC_SERVER,
            CeVIO::IID_IServiceControl2V40,
            reinterpret_cast(&pServiceControl));
        if (FAILED(result0)) {
            // 失败
            ::CoUninitialize();
            return 0;
        }

        // 启动【CeVIO AI】
        pServiceControl->StartHost(false);

        // 生成Talker实例
        CeVIO::ITalker2V40* pTalker;
        HRESULT result1 = ::CoCreateInstance(CeVIO::CLSID_Talker2V40,
            NULL,
            CLSCTX_INPROC_SERVER,
            CeVIO::IID_ITalker2V40,
            reinterpret_cast(&pTalker));
        if (FAILED(result1)) {
            // 失败
            ::CoUninitialize();
            return 0;
        }

        // 设定角色
        pTalker->Cast = "さとうささら";

        // （例）设定音量
        pTalker->Volume = 100;

        // （例）设定语调
        pTalker->ToneScale = 100;

        // （例）播放
        CeVIO::ISpeakingState2Ptr pState = pTalker->Speak("こんにちは");
        pState->Wait();

        // （例）获取音素数据
        CeVIO::IPhonemeDataArray2Ptr pPhonemes = pTalker->GetPhonemes("はじめまして");

        // 释放Talker
        pTalker->Release();

        // 关闭【CeVIO AI】
        pServiceControl->CloseHost(0);

        // 释放ServiceControl
        pServiceControl->Release();

        // COM使用结束
        ::CoUninitialize();

        return 0;
    }
    ```
    
    [CeVIO_AI_ComTest(1.1.0).zip](https://cevio.jp/storage/cevio_ai/CeVIO_AI_ComTest(1.1.0).zip)

    该压缩包内包含了上面的示例项目工程。解压后，请使用 Visual Studio 2019 或更高版本打开该项目。

=== "VBScript"

    ```vbs
    Dim service
    Set service = CreateObject("CeVIO.Talk.RemoteService2.ServiceControl2V40")
    service.StartHost(false)

    Dim talker
    Set talker = CreateObject("CeVIO.Talk.RemoteService2.Talker2V40")

    talker.Cast = "さとうささら"
    talker.Components.ByName("普通").Value = 50
    talker.Components.ByName("元気").Value = 50

    Dim state
    Set state = talker.Speak("さとうささらです。")
    state.Wait

    WScript.Sleep 1000

    talker.ToneScale = 80
    Set state = talker.Speak("スクリプトからもしゃべれます。")
    state.Wait

    service.CloseHost(0)
    ```

    [CeVIO_AI_VbsTest(1.0.1).zip](https://cevio.jp/storage/cevio_ai/CeVIO_AI_VbsTest(1.0.1).zip)

    该压缩包内包含了上面的示例脚本。解压后，请通过 Windows 命令提示符运行。
