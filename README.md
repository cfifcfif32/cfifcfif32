supabase
```csharp


hazis_mastr_polsEntities db = new hazis_mastr_polsEntities();
public MainWindow()
{
    InitializeComponent();
    List<Партнеры> a = db.Партнеры.ToList();
    for (int i = 0; i < a.Count; i++)
    {
        list.Items.Add($"{a[i].Имя} {a[i].Фамилия}");
    }
    
}
private void TextBox_TextChanged(object sender, TextChangedEventArgs e)
{
    string searchText = textBox.Text;
    var filteredEmployees = db.Партнеры.Where(x => (x.Имя + x.Фамилия).Contains(searchText)).ToList();
    list.Items.Clear();
    for (int i = 0; i < filteredEmployees.Count; i++)
    {
        list.Items.Add($"{filteredEmployees[i].Имя} {filteredEmployees[i].Фамилия}");
    }

}
List<Тип_материала> str = new List<Тип_материала>();
str = db.Тип_материала.ToList();
for (int i = 0; i < str.Count; i++)
{
    combox.Items.Add(str[i].Наименование);
}

 float materialDamage = (float)db.Тип_материала.Where(x => x.id == combox.SelectedIndex+1).FirstOrDefault().Процент_брака;


































```
```csharp

public class aaaaa
{
    public string id {get ; set;}
    public string имя { get; set; }
    public string фамлия  { get; set; }

}
orgtex2Entities db = new orgtex2Entities();
List<aaaaa> aaaaas = new List<aaaaa>();
public MainWindow()
{
   
    List<Сотрудник> сотрудник = db.Сотрудник.ToList();
    
    InitializeComponent();
    for (int i = 0; i < сотрудник.Count; i++)
    {
        aaaaas.Add(new aaaaa
        {
            id = сотрудник[i].id.ToString(),
            имя = сотрудник[i].Должность.должность1,
            фамлия = сотрудник[i].Имя,

        });
        myListView1.ItemsSource = aaaaas;
    }
}





private void TextBox_TextChanged(object sender, TextChangedEventArgs e)
{

    List<Сотрудник> emp = new List<Сотрудник>();
    var filteredEmp = aaaaas.AsQueryable();

    
        filteredEmp = filteredEmp.Where(x =>
            ($"{x.id} {x.имя} {x.фамлия}").Contains(ddddd.Text));
    
    myListView1.ItemsSource = null;
    myListView1.ItemsSource = filteredEmp;
}






















```
```csharp
using Supabase; // Не забудьте добавить ссылку на библиотеку Supabase
using System;
using System.IO;
using System.Threading.Tasks;

// Определяем модель для таблицы "cities"
[Table("cities")]
class City : BaseModel
{
    [PrimaryKey("id", false)]
    public int Id { get; set; }
    
    [Column("name")]
    public string Name { get; set; }
    
    [Column("country_id")]
    public int CountryId { get; set; }
}

class Program
{
    private static Supabase.Client supabase;

    static async Task Main(string[] args)
    {
        // Инициализация клиента Supabase
        var url = Environment.GetEnvironmentVariable("SUPABASE_URL"); // URL вашего проекта Supabase
        var key = Environment.GetEnvironmentVariable("SUPABASE_KEY"); // Публичный ключ вашего проекта Supabase
        var options = new Supabase.SupabaseOptions { AutoConnectRealtime = true };
        supabase = new Supabase.Client(url, key, options);
        await supabase.InitializeAsync();

        // Добавление записи в таблицу "cities"
        var newCity = new City { Name = "The Shire", CountryId = 554 };
        await supabase.From<City>().Insert(newCity);
        Console.WriteLine("Запись добавлена: " + newCity.Name);

        // Чтение всех записей из таблицы "cities"
        var result = await supabase.From<City>().Get();
        var cities = result.Models;
        Console.WriteLine("Список городов:");
        foreach (var city in cities)
        {
            Console.WriteLine($"- {city.Name} (ID: {city.Id})");
        }

        // Чтение записи с фильтром
        var filteredResult = await supabase.From<City>()
            .Where(x => x.Name == "Bali")
            .Get();
        Console.WriteLine("Города с именем 'Bali':");
        foreach (var city in filteredResult.Models)
        {
            Console.WriteLine($"- {city.Name} (ID: {city.Id})");
        }

        // Обновление записи
        var update = await supabase.From<City>()
            .Where(x => x.Name == "Auckland")
            .Set(x => x.Name, "Middle Earth")
            .Update();
        Console.WriteLine("Запись обновлена.");

        // Удаление записи
        await supabase.From<City>()
            .Where(x => x.Id == 342) // Укажите ID записи, которую хотите удалить
            .Delete();
        Console.WriteLine("Запись удалена.");

        // Работа с хранилищем
        // Создание нового хранилища
        var bucket = await supabase.Storage.CreateBucket("avatars");
        Console.WriteLine("Создано хранилище: avatars");

        // Загрузка файла в хранилище
        var imagePath = Path.Combine("Assets", "fancy-avatar.png"); // Укажите путь к вашему файлу
        await supabase.Storage.From("avatars")
            .Upload(imagePath, "fancy-avatar.png", new FileOptions { CacheControl = "3600", Upsert = false });
        Console.WriteLine("Файл загружен в хранилище.");

        // Получение списка файлов в хранилище
        var objects = await supabase.Storage.From("avatars").List();
        Console.WriteLine("Список файлов в хранилище:");
        foreach (var obj in objects)
        {
            Console.WriteLine($"- {obj.Name}");
        }
    }
}

```
```csharp
List<Производитель> str = db.Производитель.ToList();
for (int i = 0; i < str.Count; i++)
{
    avtor.Items.Add(str[i].Наименование);
}



List<Заявки> zaiavki = db.Заявки.Where(x => x.тип == 1).ToList()
```
```csharp
private void TextBox_TextChanged(object sender, TextChangedEventArgs e)
{
    list.Items.Clear();
    List<Товар> listt = db.Товар.Where(x => x.Название_товара.StartsWith(text.Text)).ToList();
    List<Производитель> xz = db.Производитель.ToList();
    for (int i = 0; i < listt.Count; i++)
    {
        var kol = listt[i];
        var zxzx = xz[i];
        StackPanel sp = new StackPanel();
        sp.Orientation = Orientation.Horizontal;

        System.Windows.Controls.Image img = new System.Windows.Controls.Image();
        string savePath = System.IO.Path.GetFullPath(@"..\..\..\Up_02\bin\Debug\images");
        savePath = System.IO.Path.Combine(savePath, kol.Фото.TrimEnd());

        BitmapImage bitmap = new BitmapImage();
        bitmap.BeginInit();
        bitmap.UriSource = new Uri(savePath);
        bitmap.EndInit();
        img.Source = bitmap;
        img.Width = 100;
        img.Height = 100;

        // Создаем еще один StackPanel для вертикального расположения названия товара и наименования производителя
        StackPanel textPanel = new StackPanel();
        textPanel.Orientation = Orientation.Vertical;

        TextBlock nazvanie = new TextBlock();
        TextBlock cena = new TextBlock();
        TextBlock opisnia = new TextBlock();
        TextBlock kicstov = new TextBlock();

        nazvanie.Margin = new Thickness(10, 5, 0, 0);
        nazvanie.FontSize = 16;
        cena.Margin = new Thickness(250, 5, 0, 5);
        cena.FontSize = 16;
        opisnia.Margin = new Thickness(15, 5, 0, 5);
        opisnia.FontSize = 16;
        kicstov.Margin = new Thickness(10, 5, 0, 5);
        kicstov.FontSize = 16;

        opisnia.Text = kol.Название_товара;
        nazvanie.Text = zxzx.Наименование.TrimEnd();
        cena.Text = $"{kol.Цена} ₽";

        // Добавляем текстовые блоки в вертикальный StackPanel
        textPanel.Children.Add(opisnia); // Название товара
        textPanel.Children.Add(nazvanie); // Наименование производителя

        // Добавляем изображение и текстовый StackPanel в основной StackPanel
        sp.Children.Add(img);
        sp.Children.Add(textPanel);
        sp.Children.Add(cena); // Если нужно, добавьте количество товара

        list.Items.Add(sp);

    }
}

```
```csharp
List<Партнеры> f = db.Партнеры.ToList();
List<Тип_партнера_ > a = db.Тип_партнера_.ToList();
List<Продукция_партнеров> v = db.Продукция_партнеров.ToList();
List<Продукция> z = db.Продукция.ToList();
double sskida = 0;
for (int i = 0; i < f.Count; i++)
{
    int last = 0;
    int part = Convert.ToInt32( f[i].id);
    int id2 = Convert.ToInt32( f[i].Тип_партнера);
    string neme =f[i].Наименование_партнера;
    WrapPanel wp = new WrapPanel();
    wp.Width = 700;
    if (db.Продукция_партнеров.FirstOrDefault(d => d.id_партнера == part) == null)
    {
    }
    else
    {
        var prouk = db.Продукция_партнеров.FirstOrDefault(d => d.id_партнера == part).Продукция;
        var skidk = Convert.ToInt32(db.Продукция_партнеров.FirstOrDefault(d => d.id_партнера == part).Количество_продукции);
        var kol = Convert.ToInt32(db.Продукция.FirstOrDefault(d => d.id == prouk).Минимальная_стоимость);
        last = kol * skidk;
    }
    string OAO = db.Тип_партнера_.FirstOrDefault(x => x.id == id2).Наименование;
        int riting = Convert.ToInt32(f[i].Рейтинг);
        string nomer = f[i].Телефон_партнера;
        string nemee = f[i].Имя;
        string famil = f[i].Фамилия;
        string Otvstvo = f[i].Отчество;
    
    
    
    if (last > 300000)
    {
        sskida = 15;
    }
    else if (last > 50000)
    {
        sskida = 10;
    }
    else if (last > 10000)
    {
        sskida = 5;
    }
    else
    {
        sskida = 0;
    }

    TextBlock type = new TextBlock
    {
        Text =  OAO + " | " + neme,
        FontSize = 16,
        Margin = new Thickness(10, 0, 0, 0),
        Width = wp.Width - 400
    };

    TextBlock discountTxt = new TextBlock
    {
        Text = sskida + "%",
        FontSize = 16,
        Margin = new Thickness(0, 0, 0, 0),
        TextAlignment = TextAlignment.Right,
        Width = wp.Width - 400,
        HorizontalAlignment = HorizontalAlignment.Right
    };

    TextBlock role = new TextBlock
    {
        Text = "Директор " + nemee +" "+ famil + " " + Otvstvo,
        FontSize = 12,
        Margin = new Thickness(10, 0, 0, 0),
        Width = wp.Width

    };

    TextBlock phone = new TextBlock
    {
        Text = "номер тилтфона: " + nomer,
        FontSize = 12,
        Margin = new Thickness(10, 0, 0, 0),
    };

    TextBlock rating = new TextBlock
    {
        Text = "Рейтинг: " + riting,
        FontSize = 12,
        Margin = new Thickness(10, 0, 0, 0),
        Width = wp.Width
    };

    wp.Children.Add(type);
    wp.Children.Add(discountTxt);
    wp.Children.Add(role);
    wp.Children.Add(phone);
    wp.Children.Add(rating);

    
    PartnerList.Items.Add(wp);
```
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
--
-

-
```csharp
using Word = Microsoft.Office.Interop.Word;


Word.Application wordApp = new Word.Application();
Word.Document wordDoc = wordApp.Documents.Open("C:\\Users\\pc\\source\\repos\\0202\\0202\\bin\\Debug" + "/obraz.docx");
Word.Bookmark bookmark = wordDoc.Bookmarks["mark"];
bookmark.Range.Text = amount;
string fileName = "C:\\Users\\pc\\source\\repos\\0202\\0202\\bin\\Debug" + $"/Квитанция_{DateTime.Now:dd.MM.yyyy}.docx";
wordDoc.SaveAs2(fileName);
wordDoc.Close();
wordApp.Quit();
MessageBox.Show($"Квитанция сохранена как {fileName}");

-
_
_
_
-
if (Cnechbox4.IsChecked == true)
{
    Class1 class1 = new Class1();
    summa += class1.MyMethod();
    вывод_крадаша.Content = "Крандаши";
}
if (Cnechbox3.IsChecked == true)
{
    Class1 class1 = new Class1();
    summa += class1.MyMethod1();
    вывод_альбома.Content = "Альбом";
}
if (Cnechbox2.IsChecked == true)
{
    Class1 class1 = new Class1();
    summa += class1.MyMethod2();
    вывод_Ластика.Content = "Ластик ";
}

public int MyMethod()
{
    int a = 50;
    return a;
    
}

[TestMethod]
public void TestMethod1()
{
    
    decimal need = 50;
    Class1 myClass = new Class1();
    decimal output = myClass.MyMethod();
    Assert.AreEqual(need, output);
}




```
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
--
-

-
-
-
-
-
-
-
-
-
-
-
-
-
-
-


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



занасить даные из лебла
int code;

public Window3(int id)

code = id;

 var uesr = db.сотрудники.FirstOrDefault(x => x.id == code);
 Name.Content = uesr.name;








