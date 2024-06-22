---
layout: single
title: "Clone Level Devil_Unlock Stages"
categories: project
tags: [clone-game]
author_profile: false
search: true
use_math: true
---

I made an algorithm to check opened stages before.

[Algorithm](https://henrychung98.github.io/project/levelDevilClone3Trash/#check-opened-stages)

I just converted to C# code with ChatGPT and fixed some issues.

File stream

```C#
using System;
using System.Collections.Generic;
using System.IO;
using UnityEditor.SceneManagement;
using UnityEngine;

public class FileStream : MonoBehaviour
{
    public int[] openedStages;
    private string filePath;
    [SerializeField] private int appendStage = 1;

    void Start()
    {
        filePath = Path.Combine(Application.persistentDataPath, "opened-stages.txt");
        CheckOpenedStages();
        CheckAndAppendStage(appendStage);
    }

    void CheckOpenedStages()
    {
        try
        {
            if (File.Exists(filePath))
            {
                string[] lines = File.ReadAllLines(filePath);
                List<int> tempStages = new List<int>();

                foreach (string line in lines)
                {
                    List<char> checkNum = new List<char>();
                    foreach (char c in line)
                    {
                        if (char.IsDigit(c))
                        {
                            checkNum.Add(c);
                        }
                    }

                    string combined = new string(checkNum.ToArray());
                    if (int.TryParse(combined, out int stage))
                    {
                        tempStages.Add(stage);
                    }

                }

                openedStages = tempStages.ToArray();
            }
            else
            {
                File.WriteAllText(filePath, "1\n");
                openedStages = new int[] { 1 };
            }
        }
        catch (Exception e)
        {
            Debug.LogError("Error reading or writing to the file: " + e.Message);
        }
    }

    void CheckAndAppendStage(int stageToCheck)
    {
        try
        {
            bool isOpened = false;

            if (File.Exists(filePath))
            {
                string[] lines = File.ReadAllLines(filePath);
                foreach (string line in lines)
                {
                    if (line.Trim() == stageToCheck.ToString())
                    {
                        isOpened = true;
                        break;
                    }
                }
            }

            if (!isOpened)
            {
                using (StreamWriter file = new StreamWriter(filePath, true))
                {
                    file.WriteLine(stageToCheck);
                }
            }
        }
        catch (Exception e)
        {
            Debug.LogError("Error reading or writing to the file: " + e.Message);
        }
    }
}

```

Stage Button

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;

public class StageBtn : MonoBehaviour
{
    [SerializeField] private string loadScene;
    [SerializeField] private int stageNum;
    [SerializeField] private FileStream FileVar;
    public LoadingScreen[] loadingScreens;


    void Start()
    {
        loadingScreens = FindObjectsOfType<LoadingScreen>();
        gameObject.SetActive(false);
        ValidateStage();

    }
    void ValidateStage(){
        foreach (var openStage in FileVar.openedStages)
            {
                if (openStage == stageNum){
                    gameObject.SetActive(true);
                    break;
                }
            }
    }

    public void LoadSelectedScene()
    {
        StartCoroutine(LoadStage());
    }

    private IEnumerator LoadStage(){
        foreach (var loadingScreen in loadingScreens)
            {
                loadingScreen.closeIt = true;
                loadingScreen.openIt = false;
            }

        yield return new WaitForSeconds(1f);
        SceneManager.LoadScene(loadScene);
    }
}

```
