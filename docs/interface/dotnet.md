---
title: 用作 .NET 程序集
author: 夜輪風超絶技巧変奏曲
category: interface
layout: post
---
原文：[CeVIO AI ユーザーズガイド ┃ .NETアセンブリとして利用](https://cevio.jp/guide/cevio_ai/interface/dotnet/)

---
C# 等 .NET 程序的接口。

可以使用专用 API 精细地控制情绪、状态等。

## API 规范

```cs
// 提供读说功能。
class Talker2
{
    uint Volume { get; set; }
    // 获取或设置音量（0～100）。

    uint Speed { get; set; }
    // 获取或设置语速（0～100）。

    uint Tone { get; set; }
    // 获取或设置音高（0～100）。

    uint Alpha { get; set; }
    // 获取或设置音色（0～100）。

    uint ToneScale { get; set; }
    // 获取或设置音调（0～100）。※版本4.0.7.0追加。

    TalkerComponentCollection2 Components { get; }
    // 获取当前角色的情绪参数。
    // 　内容会随着角色变化。
    // 　例1『さとうささら』→ "普通", "元気", "怒り", "哀しみ"
    // 　例2『小春六花』→ "嬉しい", "普通", "怒り", "哀しみ", "落ち着き"

    string Cast { get; set; }
    // 获取或设置角色。

    static string[] AvailableCasts { get; }
    // 获取可以使用的角色名。
    // 备注：
    // 　能获取到的角色取决于已安装的音源。

    SpeakingState2 Speak(string text);
    // 开始播放指定的台词。
    // 参数：
    // 　text - 台词。
    // 返回值：
    // 　表示播放状态的对象。
    // 备注：
    // 　该方法返回而不等待播放结束。
    // 　要等待播放结束，请调用返回值 (SpeakingState) 的 Wait。

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

    PhonemeData2[] GetPhonemes(string text);
    // 获取指定台词的音素单位的数据。
    // 参数：
    // 　text - 台词。
    // 返回值：
    // 　音素单位的数据。
    // 备注：
    // 　可以用于对口型。

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
class TalkerComponentCollection2
{
    int Count { get; }
    // 获取元素的数量。

    TalkerComponent2 this[int index] { get; }
    // 获取具有指定索引的元素。
    // 参数：
    // 　index - 索引。
    // 返回值：
    // 　元素。

    TalkerComponent2 this[string name] { get; }
    // 获取具有指定名称的元素。
    // 参数：
    // 　name - 名字。
    // 返回值：
    // 　元素。
}

// 情绪参数的单位对象。
class TalkerComponent2
{
    string Id { get; }
    // 获取标识符。

    string Name { get; }
    // 获取情绪的名字。

    uint Value { get; set; }
    // 获取或设置情绪的值（0～100）。
}

// 表示播放状态的对象。
class SpeakingState2
{
    bool IsCompleted { get; }
    // 获取播放的状态（是否完成）。
    // 完成的情况返回true。（包括失败在内）其他情况返回false。

    bool IsSucceeded { get; }
    // 获取播放的状态（是否成功）。
    // 成功时返回true。其他情况返回false。

    void Wait();
    // 等待播放结束。

    void Wait(double timeout);
    // 等待播放结束。
    // 参数：
    // 　timeout - 最大等待时间。单位是秒。（0以下为无限）
}

// 表示音素数据单位的对象。
class PhonemeData2
{
    string Phoneme { get; }
    // 获取音素。

    double StartTime { get; }
    // 获取开始时间。单位是秒。

    double EndTime { get; }
    // 获取结束时间。单位是秒。
}

// 提供【CeVIO AI】的控制功能。
static class ServiceControl2
{
    static string HostVersion { get; }
    // 获取【CeVIO AI】的客户端版本。

    static bool IsHostStarted { get; }
    // 获取【CeVIO AI】的可访问情况。

    static HostStartResult StartHost(bool noWait);
    // 启动【CeVIO Creative Studio】。如果已启动则无效。
    // 参数：
    // 　noWait - true时仅启动。关于可访问情况，可以通过 IsHostStarted 确认。
    // 　　　　　　false时不会返回控制，直到启动后允许外部访问后。
    // 返回值：
    // 　结果代码。

    static void CloseHost(HostCloseMode mode = HostCloseMode.Default);
    // 请求退出【CeVIO Creative Studio】。
    // 参数：
    // 　mode - 处理模式。
}

// 表示 StartHost() 的结果代码。
enum HostStartResult
{
    Succeeded = 0,
    // 成功。包括已启动的情况。

    NotRegistered = -1,
    // 无法确认安装状态。

    FileNotFound = -2,
    // 找不到可执行文件。

    StartingFailed = -3,
    // 无法启动进程。

    HostError = -4
    // 应用程序在启动后因错误而终止。
}

// 表示 CloseHost() 的处理代码。
enum HostCloseMode
{
    Default = 0
    // 如果【CeVIO AI】正在编辑，可以保存，取消退出等。
}
```

## 示例项目

=== "C#"

    ```cs
    using CeVIO.Talk.RemoteService2;

    namespace CeVIOCreativeStudioDotNetTest
    {
        class Program
        {
            static void Main(string[] args)
            {
                // 启动【CeVIO AI】
                ServiceControl2.StartHost(false);

                // 生成Talker实例
                Talker2 talker = new Talker2();

                // 设定角色
                talker.Cast = "さとうささら";

                // （例）设定音量
                talker.Volume = 100;

                // （例）设定语调
                talker.ToneScale = 100;

                // （例）播放
                SpeakingState2 state = talker.Speak("こんにちは");
                state.Wait();

                // （例）音素数据的跟踪输出
                PhonemeData2[] phonemes = talker.GetPhonemes("はじめまして");
                foreach (var phoneme in phonemes)
                {
                    System.Diagnostics.Trace.WriteLine(
                        "" + phoneme.Phoneme + 
                        " " + phoneme.StartTime + 
                        " " + phoneme.EndTime);
                }

                // 关闭【CeVIO AI】
                ServiceControl2.CloseHost();
            }
        }
    }
    ```

    [CeVIO_AI_DotNetTest(1.1.0).zip](https://cevio.jp/storage/cevio_ai/CeVIO_AI_DotNetTest(1.1.0).zip)

    该压缩包内包含了上面的示例项目工程。解压后，请使用 Visual Studio 2019 或更高版本打开该项目。
