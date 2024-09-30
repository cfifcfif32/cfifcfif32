https://disk.yandex.ru/d/IX-eZQ8HUIZ84Q/Теория



резерв ссылка https://disk.yandex.ru/d/n045AB_wl7-pCg/МДК%2001.01%20(ИС-21-3%2C3к).zip




с бдS
var user = db.сотрудники.FirstOrDefault(x => x.login == Login && x.password == password);

int type = (int)user.type;
int code = user.id;

Историязахода user = new Историязахода()
{
Логин = user.login,
Датазахода = date,
Попытка_входа = 1
}
db.Историязахода.Add(user);
db.SaveChanges();




--------------------------------------------------------------

int elementint;
double full_summ;
public MainWindow()
{
    InitializeComponent();
}

List<книги_> books;

List<заказ> check;

List<позиция> pos;
книгиEntities1 db = new книгиEntities1();
List<int> counts = new List<int>();
List<int> pos_count = new List<int>();


private void MyImage_MouseDown(object sender, MouseButtonEventArgs e)
{
    Point mousePosition = Mouse.GetPosition(this);
    IInputElement element = InputHitTest(mousePosition);
    string elementName = (element as FrameworkElement)?.Uid;

    elementint = Convert.ToInt32(elementName);

    Image img = new Image();
    string savePath = System.IO.Path.GetFullPath(@"Source");
    savePath = savePath + "\\" + books[elementint - 1].Изображение + ".jpg";
    BitmapImage bitmap = new BitmapImage();
    bitmap.BeginInit();
    bitmap.UriSource = new Uri(savePath);
    bitmap.EndInit();

    description.Text = books[elementint - 1].Описание;
    ImageView.Source = bitmap;
    cost.Content = "Цена: " +  books[elementint - 1].Цена;
    count.Text = Convert.ToString(counts[elementint-1]);

}


private void Window_Loaded(object sender, RoutedEventArgs e)
{
    description.IsReadOnly = true;
    count.IsReadOnly = true;
    books = db.книги_.ToList();
    check = db.заказ.ToList();
    pos = db.позиция.ToList();
    for (int i = 0; i < books.Count; i++)
    {
        //костыли))
        counts.Add(0);


        WrapPanel wp = new WrapPanel();
        Image img = new Image();
        Label labelName = new Label();

        wp.Height = 308;
        wp.Width = 200;

        labelName.Content = books[i].Название;

        string savePath = System.IO.Path.GetFullPath(@"Source");
        savePath = savePath + "\\" + books[i].Изображение + ".jpg";
        BitmapImage bitmap = new BitmapImage();
        bitmap.BeginInit();
        bitmap.UriSource = new Uri(savePath);
        bitmap.EndInit();
        img.Source = bitmap;

        img.MouseDown += new MouseButtonEventHandler(MyImage_MouseDown);
        img.Height = 250;
        img.Width = 200;

        img.Uid = books[i].код.ToString();

        wp.Children.Add(img);
        wp.Children.Add(labelName);

        ListView.Items.Add(wp);
    }
}

private void plus_Click(object sender, RoutedEventArgs e)
{
    counts[elementint-1] += 1;
    full_summ += Convert.ToDouble(books[elementint-1].Цена);
    count.Text = Convert.ToString(counts[elementint - 1]);
    summ.Content = "итого: " + full_summ;
}

private void minus_Click(object sender, RoutedEventArgs e)
{
    if (Convert.ToInt32(count.Text) > 0)
    {
        counts[elementint - 1] -= 1;
        full_summ -= Convert.ToDouble(books[elementint-1].Цена);
        count.Text = Convert.ToString(counts[elementint - 1]);
        summ.Content = "итого: " + full_summ;
    }
    else
    {
        MessageBox.Show("хотите сдать книгу обратно?)");
    }
}
private void Repwo(string subToReplace, string text, Word.Document worddoc)
{
    var range = worddoc.Content;
    range.Find.ClearFormatting();
    range.Find.Execute(FindText: subToReplace, ReplaceWith: text);
}
private void Button_Click(object sender, RoutedEventArgs e)
{
    List<заказ> zakazzz;
    zakazzz = db.заказ.ToList();
    int kod = zakazzz.Last().код + 1;


    //определение переменной для использования Word

    using (книгиEntities1 baza = new книгиEntities1())
    {
        
        for (int i = 0; i < books.Count; i++)
        {
            if (counts[i] != 0)
            {
                var position = new позиция
                {
                    код_позиции = pos.Last().код_позиции+1,
                    код_книги = i+1,
                    количество = counts[i]
                };
                MessageBox.Show("добавили поз");
                baza.позиция.Add(position);
                baza.SaveChanges();
                pos_count.Add(i+1);
                var zaka = new заказ
                {
                    код = kod,
                    код_позиции = pos.Last().код_позиции + 1,
                    дата = DateTime.Now,
                    итого = full_summ,

                };

                MessageBox.Show(kod.ToString());
                baza.заказ.Add(zaka);
                baza.SaveChanges();

            }

        }
        


        
        //var check = new заказ
        //{

        //};
        
    }
   // MessageBox.Show("начинаеца ворд");
   // var WordApp = new Word.Application();
   // WordApp.Visible = false;
   // // делаем диалог выбора папки, в которую будет сохранятся билет
   // var Worddoc = WordApp.Documents.Open(Environment.CurrentDirectory +
   // @"\check.docx");
   // Repwo("{number}", check.Last().код.ToString(), Worddoc);
   // Repwo("{date}", DateTime.Now.ToString(), Worddoc);




   //// Repwo("{books}", pos, Worddoc);
   // Repwo("{final}", full_summ.ToString(), Worddoc);
   // Worddoc.SaveAs2(Environment.CurrentDirectory + @"\билет новый.docx");
   // MessageBox.Show("Билет сохранен!");











Капчя

int attempt = 0;
attempt++;
string allowchar;
allowchar = "A,B,C,D,E,F,G,H,I,J,K,L,M,N,O,P,Q,R,S,T,U,V,W,X,Y,Z";
allowchar += "a,b,c,d,e,f,g,h,i,j,k,l,m,n,o,p,q,r,s,t,u,v,w,y,z";
allowchar += "1,2,3,4,5,6,7,8,9,0";
char[] a = { ',' };
string[] ar = allowchar.Split(a);


    
string temp;
Random r = new Random();


for (int i = 0; i < 4; i++)
{
    temp = ar[(r.Next(0, ar.Length))];
    pwd += temp;
}




штрих код

string date_in_string = DateTime.Now.Day.ToString() + DateTime.Now.Month.ToString() + DateTime.Now.Year.ToString();
MessageBox.Show(date_in_string);
System.Drawing.Image image = null;
//переменная для штрих-кода
BarcodeLib.Barcode b = new BarcodeLib.Barcode();
//Фон штрих-кода
b.BackColor = System.Drawing.Color.White;
//Цвет шрих-кода
b.ForeColor = System.Drawing.Color.Black;
//наличие текста на штрих-коде
b.IncludeLabel = true;
//Положение кода на картинке (слева, по центру, справа)
b.Alignment = BarcodeLib.AlignmentPositions.CENTER;
//Положение текста на картинке
b.LabelPosition = BarcodeLib.LabelPositions.BOTTOMCENTER;
//Формат изображения
b.ImageFormat = System.Drawing.Imaging.ImageFormat.Jpeg;
//Настройки шрифта
System.Drawing.Font font = new System.Drawing.Font("verdana", 10f);
b.LabelFont = font;
//Настройка высоты изображения (в пикселях)
b.Height = 100;
//Настройка ширины изображения (в пикселях)
b.Width = 200;
//Генерация изображения
kod_rondom += date_in_string;
image = b.Encode(BarcodeLib.TYPE.CODE128C, kod_rondom);

image.Save(@"C:\Users");


















![IMG_6260](https://github.com/cfifcfif32/cfifcfif32/assets/173002505/0037aac3-4361-4967-912e-a0a184adee5e)































----------------------------------------------------------------------------------------------------------------------
using System;
using System.Collections.Generic;
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
using Word = Microsoft.Office.Interop.Word;

namespace WpfApp2
{
    /// <summary>
    /// Логика взаимодействия для MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }
        booksEntities db = new booksEntities();
        List<Книги_> bookss;
        int selected = 0;
        private void listView_SelectionChanged(object sender, SelectionChangedEventArgs e)
        {
            BitmapImage bitimg = new BitmapImage();
            string filename = System.IO.Path.GetFullPath(@"sourse");
            filename = filename + "\\" + bookss[listView.SelectedIndex].Изображение + ".jpg";
            bitimg.BeginInit();
            bitimg.UriSource = new Uri(filename);
            bitimg.EndInit();

            textBox.Text = bookss[listView.SelectedIndex].Описание;
            image.Source = bitimg;
            selected = listView.SelectedIndex;
        }

        private void Window_Loaded(object sender, RoutedEventArgs e)
        {
            bookss = db.Книги_.ToList();

            for (int i = 0; i < bookss.Count; i ++)
            {
                WrapPanel wp = new WrapPanel();

                Image img = new Image();
                Label labelname = new Label();
                BitmapImage bitimg = new BitmapImage();

                wp.Height = 200;
                wp.Width = 180;

                labelname.Content = bookss[i].Название;

                string filename = System.IO.Path.GetFullPath(@"sourse");
                filename = filename + "\\" + bookss[i].Изображение + ".jpg";
                bitimg.BeginInit();
                bitimg.UriSource = new Uri(filename);
                bitimg.EndInit();


                img.Source = bitimg;

                img.Width = 180;
                img.Height = 160;

                wp.Children.Add(img);
                wp.Children.Add(labelname);

                listView.Items.Add(wp);

            }
        }
        private void Repwo(string subToReplace, string text, Word.Document worddoc)
        {
            var range = worddoc.Content;
            range.Find.ClearFormatting();
            range.Find.Execute(FindText: subToReplace, ReplaceWith: text);
        }
        private void button_Click(object sender, RoutedEventArgs e)
        {
             MessageBox.Show("начинаеца ворд");
             var WordApp = new Word.Application();
             WordApp.Visible = false;
             //делаем диалог выбора папки, в которую будет сохранятся билет
             var Worddoc = WordApp.Documents.Open(Environment.CurrentDirectory +
             @"\check.docx");
             Repwo("{number}", "1", Worddoc);
             Repwo("{date}", DateTime.Now.ToString(), Worddoc);
             Repwo("{count}", "13", Worddoc);




             Repwo("{book}",bookss[listView.SelectedIndex].Автор, Worddoc);
             Repwo("{final}", "214", Worddoc);
             Worddoc.SaveAs2(Environment.CurrentDirectory + @"\билет новый.docx");
             MessageBox.Show("Билет сохранен!");
        }
    }
}
__________________________________________________________________________________________
поиск в листе чериз текст бокс

 string search = log.Text;
 if (log.Text != "")
 {
     var foundUsers = users.Where(x => x.Логин.StartsWith(search)).ToList();
     listUsers.ItemsSource = foundUsers;
 }
 else
 {
     listUsers.ItemsSource = users;
 }




код для чтобы можно было писат толька числа

try
{
Convet.ToInt32(text1.Text);
//делаем
}
catch
{
text = "";
} 
![image](https://github.com/user-attachments/assets/b531fae0-aac5-42ed-a839-ad0ea2156b29)

List<книги_> lol = db.книги_.ToList();
for (int i = 0; i < lol.Count; i++)
{

    //Создаем элемент плитки для отображения
    WrapPanel wp = new WrapPanel();
    System.Windows.Controls.Image ing = new System.Windows.Controls.Image();
    Label labelName = new Label();
    //Настройка плитки.

    wp.Height = 300;
    wp.Width = 200;

    //Настройка Лейбла(Названия)

    labelName.Content = lol[i].Название; // в List загружены данные о книгах. i - индекс элемента, 1 - индекс столбца

    // Настройка Изображений.
    // Путь, изображения должны лежать в папке проекта Source.

    string savePath = System.IO.Path.GetFullPath(@"C:\Users\cfifc\source\repos\Bookkk\Bookkk\Source");
    savePath = savePath + "\\" + lol[i].Изображение+".jpg"; //i - индекс элемента, 2 - индекс столбца с изобракением.
    BitmapImage bitmap = new BitmapImage();
    bitmap.BeginInit();
    bitmap.UriSource = new Uri(savePath);
    bitmap.EndInit();
    ing.Source = bitmap;
    // Программно добавляем сробытие для плитки.
    ing.MouseDown += new MouseButtonEventHandler(list_MouseDown);
    //Настройка размера изображения.

    ing.Height = 250;
    ing.Width = 200;
    // Говорим изображению, чтобы в сасих данных хранил Id элемента, і - индекс элемекта, е - индекс столбца

    ing.Uid = lol[i].id.ToString();

    // Отправляем изображение и наименование в плитку(Дочерние в родительские).

    wp.Children.Add(ing);
    wp.Children.Add(labelName);
    //Добавляем плитку в ListView.
    list1.Items.Add(wp);
}
![image](https://github.com/user-attachments/assets/a69cda83-ae4d-4d2f-8d0d-5d1b016a4d92)

            List<книги_> lol = db.книги_.ToList();
            System.Windows.Point mousePosition = Mouse.GetPosition(this);

            IInputElement element = InputHitTest(mousePosition);

            string elementNeme = (element as FrameworkElement) ?. Uid;
            int elementNeme1 = Convert.ToInt32(elementNeme) - 1;
            string savePath = System.IO.Path.GetFullPath(@"C:\Users\cfifc\source\repos\Bookkk\Bookkk\Source");
            savePath = savePath + "\\" + lol[elementNeme1].Изображение + ".jpg"; //i - индекс элемента, 2 - индекс столбца с изобракением.
            BitmapImage bitmap = new BitmapImage();
            bitmap.BeginInit();
            bitmap.UriSource = new Uri(savePath);
            bitmap.EndInit();
            im.Source = bitmap;
            lebel.Content = lol[elementNeme1].Название;
![image](https://github.com/user-attachments/assets/e702ed2c-efaf-476a-a7bf-1a24baed5288)

![image](https://github.com/user-attachments/assets/bec76961-bb13-4ba9-aa2c-87129208ebba)
string search = box.Text;
if (box.Text != "")
{
    list1.Items.Clear();
    List<книги_> lol = db.книги_.ToList();
    lol = lol.Where(x => x.Название.StartsWith(search)).ToList();
    for (int i = 0; i < lol.Count; i++)
    {

        //Создаем элемент плитки для отображения
        WrapPanel wp = new WrapPanel();
        System.Windows.Controls.Image ing = new System.Windows.Controls.Image();
        Label labelName = new Label();
        //Настройка плитки.

        wp.Height = 300;
        wp.Width = 200;

        //Настройка Лейбла(Названия)

        labelName.Content = lol[i].Название; // в List загружены данные о книгах. i - индекс элемента, 1 - индекс столбца

        // Настройка Изображений.
        // Путь, изображения должны лежать в папке проекта Source.

        string savePath = System.IO.Path.GetFullPath(@"C:\Users\cfifc\source\repos\Bookkk\Bookkk\Source");
        savePath = savePath + "\\" + lol[i].Изображение + ".jpg"; //i - индекс элемента, 2 - индекс столбца с изобракением.
        BitmapImage bitmap = new BitmapImage();
        bitmap.BeginInit();
        bitmap.UriSource = new Uri(savePath);
        bitmap.EndInit();
        ing.Source = bitmap;
        // Программно добавляем сробытие для плитки.
        ing.MouseDown += new MouseButtonEventHandler(list_MouseDown);
        //Настройка размера изображения.

        ing.Height = 250;
        ing.Width = 200;
        // Говорим изображению, чтобы в сасих данных хранил Id элемента, і - индекс элемекта, е - индекс столбца

        ing.Uid = lol[i].id.ToString();

        // Отправляем изображение и наименование в плитку(Дочерние в родительские).

        wp.Children.Add(ing);
        wp.Children.Add(labelName);
        //Добавляем плитку в ListView.
        list1.Items.Add(wp);

    }


}
else
{
    list1.Items.Clear();
    List<книги_> lol = db.книги_.ToList();

    for (int i = 0; i < lol.Count; i++)
    {

        //Создаем элемент плитки для отображения
        WrapPanel wp = new WrapPanel();
        System.Windows.Controls.Image ing = new System.Windows.Controls.Image();
        Label labelName = new Label();
        //Настройка плитки.

        wp.Height = 300;
        wp.Width = 200;

        //Настройка Лейбла(Названия)

        labelName.Content = lol[i].Название; // в List загружены данные о книгах. i - индекс элемента, 1 - индекс столбца

        // Настройка Изображений.
        // Путь, изображения должны лежать в папке проекта Source.

        string savePath = System.IO.Path.GetFullPath(@"C:\Users\cfifc\source\repos\Bookkk\Bookkk\Source");
        savePath = savePath + "\\" + lol[i].Изображение + ".jpg"; //i - индекс элемента, 2 - индекс столбца с изобракением.
        BitmapImage bitmap = new BitmapImage();
        bitmap.BeginInit();
        bitmap.UriSource = new Uri(savePath);
        bitmap.EndInit();
        ing.Source = bitmap;
        // Программно добавляем сробытие для плитки.
        ing.MouseDown += new MouseButtonEventHandler(list_MouseDown);
        //Настройка размера изображения.

        ing.Height = 250;
        ing.Width = 200;
        // Говорим изображению, чтобы в сасих данных хранил Id элемента, і - индекс элемекта, е - индекс столбца

        ing.Uid = lol[i].id.ToString();

        // Отправляем изображение и наименование в плитку(Дочерние в родительские).

        wp.Children.Add(ing);
        wp.Children.Add(labelName);
        //Добавляем плитку в ListView.
        list1.Items.Add(wp);
    }
}
------------------------------------------------------------------------------------------------------------------------------------------------------------------





пример библотеки


    public class Class1
    {
        public bool check_password(string password)
        {
            string pattern = @"^(?=.*[A-Za-z])(?=.*\d)(?=.*[^A-Za-z\d]).{8,}$";

            Regex regex = new Regex(pattern);

            return regex.IsMatch(password);
        }
        public bool check_password1(string password1)
        { 
            
            int indexOfChar = password1.IndexOf("!");
            int indexOfChar1 = password1.IndexOf("*");
            int indexOfChar2 = password1.IndexOf(" ");
            int indexOfChar3 = password1.IndexOf(";");
            if (indexOfChar != -1 && indexOfChar1 != -1 && indexOfChar2 == -1 && indexOfChar3 == -1)
            {
                if (password1.Length > 8)
                {
                    if (password1.Length < 25)
                    {

                        return true;

                    }
                    else
                    {
                        return false;
                    }
                }
                else
                {
                    return false;
                }
            }
            return false;


        }

    }
}
прмер работы


using ClassLibrary1;


Class1 a = new Class1();
string login1 = Convert.ToString(login);
string passvord1 = Convert.ToString(passvord.Text);
if (login1 !="" && passvord1 !="")
{

    if (a.check_password1(passvord1))
    {
        MessageBox.Show("мы тут ");
        Window1 aa = new Window1(bitmapImage);
        aa.Show();
        this.Close();
    }

    MessageBox.Show("ок");
}
else
{

}

--------------------------------------------------------------------------------------------------------------
Картинки 
 Window1 aa = new Window1(bitmapImage);
 aa.Show();
 this.Close();
на кнопку
// Open a file dialog to select a photo
OpenFileDialog openFileDialog = new OpenFileDialog();
openFileDialog.Filter = "Image Files (*.jpg, *.jpeg, *.png, *.bmp)|*.jpg;*.jpeg;*.png;*.bmp";
openFileDialog.InitialDirectory = Environment.GetFolderPath(Environment.SpecialFolder.MyPictures);

if (openFileDialog.ShowDialog() == true)
{
    // Get the selected file path
    string filePath = openFileDialog.FileName;

    // Load the selected photo into the Image control
    bitmapImage = new BitmapImage();
    bitmapImage.BeginInit();
    bitmapImage.UriSource = new Uri(filePath);
    bitmapImage.EndInit();
    a.Source = bitmapImage;
}

на 2 форме 
f.Source = bitmapImage;









