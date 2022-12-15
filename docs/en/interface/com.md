---
title: Used as a COM Component
author: 夜輪風超絶技巧変奏曲
category: interface
layout: post
---
Original article: [CeVIO AI ユーザーズガイド ┃ COMコンポーネントとして利用](https://cevio.jp/guide/cevio_ai/interface/com/)

---
Interface for programming with C++, VBScript, etc.

The dedicated API allows detailed control of emotions and conditions.

## API Specification

```cpp
// Provide the Talk function.
interface ITalker2V40
{
    uint Volume { get; set; }
    // Get or set volume (0~100).

    uint Speed { get; set; }
    // Get or set speed (0~100)

    uint Tone { get; set; }
    // Get or set pitch (0~100).

    uint ToneScale { get; set; }
    // Get or set intonation (0~100).

    uint Alpha { get; set; }
    // Get or set alpha (0~100).

    ITalkerComponentArray2 Components { get; }
    // Get the emotion parameters of current cast.
    // Annotation:
    // 　The parameters depending on the Cast.
    // 　example 1『さとうささら』→ "普通", "元気", "怒り", "哀しみ"
    // 　example 2『小春六花』→ "嬉しい", "普通", "怒り", "哀しみ", "落ち着き"
    // Attention: 
    // 　When using smart pointer in Visual C++ environment, this type is replaced by the following type.
    // 　ITalkerComponentArray2Ptr

    string Cast { get; set; }
    // Get or set the cast.

    IStringArray AvailableCasts { get; }
    // Get the available casts.
    // Annotation:
    // 　The available casts depend on the installed voices.
    // Attention:
    // 　When using smart pointer in Visual C++ environment, this type is replaced by the following type.
    // 　IStringArray2Ptr

    ISpeakingState2 Speak(string text);
    // Play the specified line.
    // Parameters:
    // 　text - line.
    // Return value:
    // 　An object representing the playback state.
    // Annotation:
    // 　The process returns without waiting for the end of playback.
    // 　To wait for the end of playback, call Wait of the return value (ISpeakingState2).
    // Attention:
    // 　When using smart pointer in Visual C++ environment, this type is replaced by the following type.
    // 　ISpeakingState2Ptr

    bool Stop();
    // Stop playback.
    // Return value:
    // 　true if succeed. false otherwise.

    double GetTextDuration(string text);
    // Get the length of the specified line.
    // Parameters:
    // 　text - line.
    // Return value:
    // 　Length. Unit is seconds.

    IPhonemeDataArray2 GetPhonemes(string text);
    // Get phoneme unit data of the specified line.
    // Parameters:
    // 　text - line.
    // Return value:
    // 　Phoneme unit data.
    // Annotation:
    // 　Can be used for lip sinks, etc.
    // Attention:
    // 　When using smart pointer in Visual C++ environment, this type is replaced by the following type.
    // 　IPhonemeDataArray2Ptr

    bool OutputWaveToFile(string text, string path);
    // Output the specified line to a wav file.
    // Parameters:
    // 　text - line.
    // 　path - path to be outputted.
    // Return value:
    // 　true if succeed. false otherwise.
    // Annotation:
    // 　The output format is sampling rate 48kHz, bit rate 16bit, mono.
}

// An object representing the cast's emotion parameter map.
interface ITalkerComponentArray2
{
    int Length { get; }
    // Get the number of parameters.

    ITalkerComponent2 At(int index) { get; }
    // Access the parameter at specified location index.
    // Parameters:
    // 　index - index.
    // Return value:
    // 　parameter.

    ITalkerComponent2 ByName(string name) { get; }
    // Access the parameter with the specified name.
    // Parameters:
    // 　name - name.
    // Return value:
    // 　parameter.

    ITalkerComponentArray2 Duplicate();
    // Copy the array.
    // Return value:
    // 　The index of the copied array.
}

// The object of emotion parameters unit.
interface ITalkerComponent2
{
    string Id { get; }
    // Get the identifier.

    string Name { get; }
    // Get the name of emotion. (Character code is Unicode)

    uint Value { get; set; }
    // Get or set the value of an emotion (0~100).
}

// The object representing of playback status.
interface ISpeakingState2
{
    bool IsCompleted { get; }
    // Get the playback status (whether or not playback is completed).
    // true if completed. false otherwise (failures included).

    bool IsSucceeded { get; }
    // Get the playback status (whether or not playback is succeed).
    // true if succeed. false otherwise.

    void Wait();
    // Wait for the end of playback.

    void Wait_2(double timeout);
    // Wait for the end of playback.
    // Parameters:
    // 　timeout - Maximum standby time. Unit is seconds. (Smaller than 0 means unlimited)
}

// The object representing the array of phoneme data.
interface IPhonemeDataArray2
{
    int Length { get; }
    // Get the number of elements.

    IPhonemeData2 At(int index);
    // Access the element at specified location index.
    // Parameters:
    // 　index - index.
    // Return value:
    // 　element.

    IPhonemeDataArray2 Duplicate();
    // Copy the array.
    // Return value:
    // 　The index of the copied array.
}

// The object representing the unit of phoneme data.
interface IPhonemeData2
{
    string Phoneme { get; }
    // Get the phoneme.

    double StartTime { get; }
    // Get the start time. Unit is seconds.

    double EndTime { get; }
    // Get the end time. Unit is seconds.
}

// The object representing the array of string.
interface IStringArray2
{
    int Length { get; }
    // Get the number of elements.

    string At(int index);
    // Parameters:
    // 　index - index.
    // Return value:
    // 　element.

    IStringArray2 Duplicate();
    // Copy the array.
    // Return value:
    // 　The index of the copied array.
}

// Provide the control function of [CeVIO AI].
interface IServiceControl2V40
{
    string HostVersion { get; }
    // Get the version of [CeVIO Creative Studio](1).

    string InterfaceVersion { get; }
    // Get the version of this interface.

    static bool IsHostStarted { get; }
    // Get the status whether or not [CeVIO Creative Studio] can be accessed.

    int StartHost(bool noWait);
    // Start [CeVIO Creative Studio]. Do nothing if it is already started.
    // Parameters:
    // 　noWait - true means startup only. IsHostStarted checks if it is accessible or not.
    // 　　　　　　false does not return control until it is accessible externally after startup.
    // Return value:
    // 　 0：Success. This includes the case when it has already been started.
    // 　-1：Unknown installation status.
    // 　-2：Can't find the executable file.
    // 　-3：Failed to start process.
    // 　-4：Application terminates due to an error after startup.

    void CloseHost(int mode);
    // Request [CeVIO Creative Studio] to exit.
    // Parameters:
    // 　mode - handle mode.
    // 　 0：When [CeVIO AI] is editing, it is able to save or cancel the end of the editing process.
}
```

1. Original text. Same below.

## Sample Project

=== "C++"

    ```cpp
    // Import type library 
    // * This type library is registered when installing [CeVIO AI].
    #import "libid:7E3B8901-0A65-44A0-9A9A-5F9F822D0716" 
        named_guids rename_namespace("CeVIO")

    int main()
    {
        // Initialize COM
        ::CoInitialize(NULL);

        // Create ServiceControl instance
        CeVIO::IServiceControl2V40* pServiceControl;
        HRESULT result0 = ::CoCreateInstance(CeVIO::CLSID_ServiceControl2V40,
            NULL,
            CLSCTX_INPROC_SERVER,
            CeVIO::IID_IServiceControl2V40,
            reinterpret_cast(&pServiceControl));
        if (FAILED(result0)) {
            // Failed
            ::CoUninitialize();
            return 0;
        }

        // Start CeVIO AI up
        pServiceControl->StartHost(false);

        // Create Talker instance
        CeVIO::ITalker2V40* pTalker;
        HRESULT result1 = ::CoCreateInstance(CeVIO::CLSID_Talker2V40,
            NULL,
            CLSCTX_INPROC_SERVER,
            CeVIO::IID_ITalker2V40,
            reinterpret_cast(&pTalker));
        if (FAILED(result1)) {
            // Failed
            ::CoUninitialize();
            return 0;
        }

        // Set the cast
        pTalker->Cast = "さとうささら";

        // (Example) set the volume
        pTalker->Volume = 100;

        // (Example) set the intonation
        pTalker->ToneScale = 100;

        // (Example) playback
        CeVIO::ISpeakingState2Ptr pState = pTalker->Speak("こんにちは");
        pState->Wait();

        // (Example) get the data of phonemes
        CeVIO::IPhonemeDataArray2Ptr pPhonemes = pTalker->GetPhonemes("はじめまして");

        // Release Talker
        pTalker->Release();

        // Close [CeVIO AI]
        pServiceControl->CloseHost(0);

        // Release ServiceControl
        pServiceControl->Release();

        // End of using COM
        ::CoUninitialize();

        return 0;
    }
    ```
    
    [CeVIO_AI_ComTest(1.1.0).zip](https://cevio.jp/storage/cevio_ai/CeVIO_AI_ComTest(1.1.0).zip)

    The zip contains the example project above. After unzipping, load the solution in Visual Studio 2019 or later to run it.

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

    The zip contains the example script above. After unzipping, load the solution in Windows Command Prompt to run it.
