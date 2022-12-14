---
title: Used as a .NET Assembly
author: 夜輪風超絶技巧変奏曲
category: interface
layout: post
---
Original article: [CeVIO AI ユーザーズガイド ┃ .NETアセンブリとして利用](https://cevio.jp/guide/cevio_ai/interface/dotnet/)

---
Interface for programming with .NET programs such as C#, etc.

The dedicated API allows detailed control of emotions and conditions.

## API Specification

```cs
// Provide the Talk function.
class Talker2
{
    uint Volume { get; set; }
    // Get or set volume (0~100).

    uint Speed { get; set; }
    // Get or set speed (0~100)

    uint Tone { get; set; }
    // Get or set pitch (0~100).

    uint Alpha { get; set; }
    // Get or set alpha (0~100).

    uint ToneScale { get; set; }
    // Get or set intonation (0~100). *Since version 4.0.7.0

    TalkerComponentCollection2 Components { get; }
    // Get the emotion parameters of current cast.
    // Annotation:
    // 　The parameters depending on the Cast.
    // 　example 1『さとうささら』→ "普通", "元気", "怒り", "哀しみ"
    // 　example 2『小春六花』→ "嬉しい", "普通", "怒り", "哀しみ", "落ち着き"

    string Cast { get; set; }
    // Get or set the cast.

    static string[] AvailableCasts { get; }
    // Get the available casts.
    // Annotation:
    // 　The available casts depend on the installed voices.

    SpeakingState2 Speak(string text);
    // Play the specified line.
    // Parameters:
    // 　text - line.
    // Return value:
    // 　An object representing the playback state.
    // Annotation:
    // 　The process returns without waiting for the end of playback.
    // 　To wait for the end of playback, call Wait of the return value (SpeakingState).

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

    PhonemeData2[] GetPhonemes(string text);
    // Get phoneme unit data of the specified line.
    // Parameters:
    // 　text - line.
    // Return value:
    // 　Phoneme unit data.
    // Annotation:
    // 　Can be used for lip sinks, etc.

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
class TalkerComponentCollection2
{
    int Count { get; }
    // Get the number of parameters.

    TalkerComponent2 this[int index] { get; }
    // Access the parameter at specified location index.
    // Parameters:
    // 　index - index.
    // Return value:
    // 　parameter.

    TalkerComponent2 this[string name] { get; }
    // Access the parameter with the specified name.
    // Parameters:
    // 　name - name.
    // Return value:
    // 　parameter.
}

// The object of emotion parameters unit.
class TalkerComponent2
{
    string Id { get; }
    // Get the identifier.

    string Name { get; }
    // Get the name of emotion.

    uint Value { get; set; }
    // Get or set the value of an emotion (0~100).
}

// The object representing of playback status.
class SpeakingState2
{
    bool IsCompleted { get; }
    // Get the playback status (whether or not playback is completed).
    // true if completed. false otherwise (failures included).

    bool IsSucceeded { get; }
    // Get the playback status (whether or not playback is succeed).
    // true if succeed. false otherwise.

    void Wait();
    // Wait for the end of playback.

    void Wait(double timeout);
    // Wait for the end of playback.
    // Parameters:
    // 　timeout - Maximum standby time. Unit is seconds. (Smaller than 0 means unlimited)
}

// The object representing the unit of phoneme data.
class PhonemeData2
{
    string Phoneme { get; }
    // Get the phoneme.

    double StartTime { get; }
    // Get the start time. Unit is seconds.

    double EndTime { get; }
    // Get the end time. Unit is seconds.
}

// Provide the control function of [CeVIO AI].
static class ServiceControl2
{
    static string HostVersion { get; }
    // Get the version of [CeVIO AI].

    static bool IsHostStarted { get; }
    // Get the status whether or not [CeVIO AI] can be accessed.

    static HostStartResult StartHost(bool noWait);
    // Start [CeVIO AI]. Do nothing if it is already started.
    // Parameters:
    // 　noWait - true means startup only. IsHostStarted checks if it is accessible or not.
    // 　　　　　　false does not return control until it is accessible externally after startup.
    // Return value:
    // 　 Result code.

    static void CloseHost(HostCloseMode mode = HostCloseMode.Default);
    // Request [CeVIO AI] to exit.
    // Parameters:
    // 　mode - handle mode.
}

// Result code representing for StartHost().
enum HostStartResult
{
    Succeeded = 0,
    // Success. This includes the case when it has already been started.

    NotRegistered = -1,
    // Unknown installation status.

    FileNotFound = -2,
    // Can't find the executable file.

    StartingFailed = -3,
    // Failed to start process.

    HostError = -4
    // Application terminates due to an error after startup.
}

// Result code representing for CloseHost().
enum HostCloseMode
{
    Default = 0
    // When [CeVIO AI] is editing, it is able to save or cancel the end of the editing process.
}
```

## Sample Project

=== "C#"

    ```cs
    using CeVIO.Talk.RemoteService2;

    namespace CeVIOCreativeStudioDotNetTest
    {
        class Program
        {
            static void Main(string[] args)
            {
                // Start CeVIO AI up
                ServiceControl2.StartHost(false);

                // Create Talker instance
                Talker2 talker = new Talker2();

                // Set the cast
                talker.Cast = "さとうささら";

                // (Example) set the volume
                talker.Volume = 100;

                // (Example) set the intonation
                talker.ToneScale = 100;

                // (Example) playback
                SpeakingState2 state = talker.Speak("こんにちは");
                state.Wait();

                // (Example) get the data of phonemes and print
                PhonemeData2[] phonemes = talker.GetPhonemes("はじめまして");
                foreach (var phoneme in phonemes)
                {
                    System.Diagnostics.Trace.WriteLine(
                        "" + phoneme.Phoneme + 
                        " " + phoneme.StartTime + 
                        " " + phoneme.EndTime);
                }

                // Close [CeVIO AI]
                ServiceControl2.CloseHost();
            }
        }
    }
    ```

    [CeVIO_AI_DotNetTest(1.1.0).zip](https://cevio.jp/storage/cevio_ai/CeVIO_AI_DotNetTest(1.1.0).zip)

    The zip contains the example project above. After unzipping, load the solution in Visual Studio 2019 or later to run it.
