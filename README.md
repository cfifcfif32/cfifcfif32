https://disk.yandex.ru/d/IX-eZQ8HUIZ84Q/Теория








с бд
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



