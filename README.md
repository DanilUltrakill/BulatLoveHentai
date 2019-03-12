# BulatLoveHentai
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;

namespace TRPO894
{
    /// <summary>
    /// Логика взаимодействия для MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        static double proverka(int a)
        {
            try
            {
                return arg1 / Ostatok(arg1, arg2);
            }
            catch (DivideByZeroException)
            {
                throw new DivideByZeroException("Остаток от деления равен 0");
            }
            catch //универсальный обработчик
            {
                //сделать здесь что-то
                //иначе этот catch не нужен,
                //так как другие исключения и так пробросятся дальше
                throw;
            }

        }
        public MainWindow()
        {
            InitializeComponent();
           

        }
       
        private void TextBox_TextChanged(object sender, TextChangedEventArgs e)
        {
            
        }

        private void Button_Click(object sender, RoutedEventArgs e)
        {
            try //блок в котором может возникнуть исключение
            {
                int a = int.Parse(tb1.Text);

                if (a == 2)
                    list.Items.Add(tb1.Text);
                if (a == 1)
                    list.Items.Add(tb1.Text);
                   
                for (int i = 2; i < a; i++)
                {                    
                    if (a % i == 0)
                    {
                        tb2.Text = ")";
                        break;
                    }
                    if (i == a - 1)
                        list.Items.Add(tb1.Text);
                }
            }
            catch (DivideByZeroException) //реакция на деление на нуль
            {
                tb2.Text = ")";
            }
            catch (FormatException) //реакция на неверный ввод
            {
                tb2.Text = ")";
            }
           
        }

        private void tb1_MouseDoubleClick(object sender, MouseButtonEventArgs e)
        {
            tb1.Text = "";
            tb2.Text = "";
        }

        private void list_SelectionChanged(object sender, SelectionChangedEventArgs e)
        {

        }

        private void mb2_Click(object sender, RoutedEventArgs e)
        {
            //создание диалога
            Microsoft.Win32.OpenFileDialog dlg = new Microsoft.Win32.OpenFileDialog();
            //настройка параметров диалога
            dlg.FileName = "Document"; // Default file name
            dlg.DefaultExt = ".txt"; // Default file extension
            dlg.Filter = "Text documents (.txt)|*.txt"; // Filter files by extension
                                                        //вызов диалога
            dlg.ShowDialog();
            //получе выбранного имени файла

            try //блок в котором может возникнуть исключение
            {
                string line;
                System.IO.StreamReader file = new System.IO.StreamReader(dlg.FileName);

                while ((line = file.ReadLine()) != null)
                {

                    int a = int.Parse(line);

                    if (a == 2)
                        list.Items.Add(line);
                    if (a == 1)
                        list.Items.Add(line);

                    for (int i = 2; i < a; i++)
                    {
                        if (a % i == 0)
                        {
                            tb2.Text = ")";
                            break;
                        }
                        if (i == a - 1)
                            list.Items.Add(line);
                    }
                }
                file.Close();
            }
            catch (DivideByZeroException) //реакция на деление на нуль
            {
                tb2.Text = ")";
            }
            catch (FormatException) //реакция на неверный ввод
            {
                tb2.Text = ")";
            }
            catch(FileNotFoundException)
            {
                tb2.Text = ")";
            }
            
        }

            private void mb1_Click(object sender, RoutedEventArgs e)
        {
            //создание диалога
            Microsoft.Win32.SaveFileDialog dlg = new Microsoft.Win32.SaveFileDialog();
            //настройка параметров диалога
            dlg.FileName = "Document"; // Default file name
            dlg.DefaultExt = ".txt"; // Default file extension
            dlg.Filter = "Text documents (.txt)|*.txt"; // Filter files by extension
                                                        //вызов диалога
            dlg.ShowDialog(); //получение выбранного имени файла
            string[] lines = list.Items.OfType<string>().ToArray();
            using (StreamWriter outputFile = new StreamWriter(dlg.FileName))
            {
                //lines – массив строк
                foreach (string line in lines)
                    outputFile.WriteLine(line);
            }
        }
    }
}
