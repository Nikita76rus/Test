 
//////////////////////////////////UNIT-TEST/////////////////////////////////////////////
bool expected = true;
String c = new String();
bool actual = c.First(result);
Assert.AreEqual(expected, actual);

//////////////////////////////////REGISTRATION//////////////////////////////////////////
void autentification(object sender, RoutedEventArgs e)
        {
            try
            {
                string query = "Select Login, Password, Role from Users where Login ='" + tLogin.Text.Trim() + "' and Password ='" + tPass.Password.Trim() + "'";
                SqlConnection myConnection = new SqlConnection(ConString);
                SqlCommand sda = new SqlCommand(query, myConnection);
                myConnection.Open();
                SqlDataReader rd = sda.ExecuteReader();
                string Login = "null";
                string Password = "null";
                string Role = "null";
                while (rd.Read())
                {
                    Login = rd.GetString(0);
                    Password = rd.GetString(1);
                    Role = rd.GetString(2);
                }
                myConnection.Close();
                if ((Login == "null") || (Password == "null"))
                {
                    MessageBox.Show(string.Format("Данные не введены или вы не зарегистрировались"), "Предупреждение", MessageBoxButton.OK, MessageBoxImage.Warning);

                }
                else
                {

                    MessageBox.Show(string.Format("Вы успешно вошли в систему"), "Сообщение", MessageBoxButton.OK, MessageBoxImage.Information);
                    if (Role == "Supervisor")
                    {
                        Supervisor pagerS = new Supervisor();
                        pagerS.Show();
                        this.Close();
                    }
                    if (Role == "Client")
                    {
                        Client pagerCl = new Client();
                        pagerCl.Show();
                        this.Close();
                    }

                }
            }
            catch
            {
                MessageBox.Show(string.Format("Сервис временно недоступен"), "Ошибка входа", MessageBoxButton.OK, MessageBoxImage.Error);

            }


        }
        void registration(object sender, RoutedEventArgs e)
        {
            try
            {
                if (tLoginR.Text == "" || tNameR.Text == "" || tEmailR.Text == "" || tPassR.Password == "")
                {
                    MessageBox.Show(
                    "Пожалуйста, заполните все поля.",
                    "Предупреждение", MessageBoxButton.OK, MessageBoxImage.Warning);
                }
                else
                {

                    SqlConnection myConnection = new SqlConnection(ConString);

                    myConnection.Open();

                    string sInsSql = "Insert into Users( Login, Password, Name, Email, Role) Values('{0}', '{1}', '{2}', '{3}', '{4}')";

                    string loginR = tLoginR.Text.Trim();
                    string passwordR = tPassR.Password.Trim();
                    string nameR = tNameR.Text.Trim();
                    string emailR = tEmailR.Text.Trim();
                    string role = "Client";

                    string sInsSotr = string.Format(sInsSql, loginR, passwordR, nameR, emailR, role);
                    SqlCommand cmdIns = new SqlCommand(sInsSotr, myConnection);

                    cmdIns.ExecuteNonQuery();

                    MessageBox.Show(
                    "Регистрация прошла успешно.",
                    "Сообщение", MessageBoxButton.OK, MessageBoxImage.Information);

                    myConnection.Close();
                    authstate(sender, e);





                }
            }
            catch
            {
                MessageBox.Show(string.Format("Сервис временно недоступен"), "Ошибка регистрации", MessageBoxButton.OK, MessageBoxImage.Error);
            }

        }
//////////////////////////////////LOAD//////////////////////////////////////////
 private void Storekeeper_page1_Loaded(object sender, RoutedEventArgs e)
        {
            string sql = "SELECT Name, Color,  Drawing,  Composition, Width, Length, Price FROM Fabric";
            Table = new DataTable();
            SqlConnection connection = null;

            connection = new SqlConnection(ConString);
            SqlCommand command = new SqlCommand(sql, connection);
            adapter = new SqlDataAdapter(command);

            connection.Open();
            adapter.Fill(Table);
            Storekeep_Table.ItemsSource = Table.DefaultView;
        }

        private void ComboBox_SelectionChanged(object sender, SelectionChangedEventArgs e)
        {
            if (Keeper.Text == "Фурнитура")
            {
                string sql = "SELECT Article, Name, Color,  Drawing, Composition, Width, Length, Price FROM Fabric";
                Table = new DataTable();
                SqlConnection connection = null;

                connection = new SqlConnection(ConString);
                SqlCommand command = new SqlCommand(sql, connection);
                adapter = new SqlDataAdapter(command);

                connection.Open();
                adapter.Fill(Table);
                Storekeep_Table.ItemsSource = Table.DefaultView;
            }
            
 public class Phone
{
    public int Id { get; set; }
    public string Title { get; set; }
    public string Company { get; set; }
    public int Price { get; set; }
}

using System.Data.Entity;
 
public class MobileContext : DbContext
{
    public MobileContext(): base("DefaultConnection")
    {
 
    }
    public DbSet<Phone> Phones { get; set; }
}
 <DataGridTextColumn Binding="{Binding Title}" Header="Модель" Width="100"/>
 
   db = new MobileContext();
            db.Phones.Load(); // загружаем данные
            phonesGrid.ItemsSource = db.Phones.Local.ToBindingList(); // устанавливаем привязку к кэшу
            
             private void deleteButton_Click(object sender, RoutedEventArgs e)
        {
            if (phonesGrid.SelectedItems.Count>0)
            {
                for (int i = 0; i < phonesGrid.SelectedItems.Count; i++)
                {
                    Phone phone = phonesGrid.SelectedItems[i] as Phone;
                    if (phone != null)
                    {
                        db.Phones.Remove(phone);
                    }
                }
            }
            db.SaveChanges();
        }
///////////////////////////////////////FILE/////////////////////////////////////////
private void button1_Click(object sender, RoutedEventArgs e)
{
    // Create OpenFileDialog 
    Microsoft.Win32.OpenFileDialog dlg = new Microsoft.Win32.OpenFileDialog();



    // Set filter for file extension and default file extension 
    dlg.DefaultExt = ".png";
    dlg.Filter = "JPEG Files (*.jpeg)|*.jpeg|PNG Files (*.png)|*.png|JPG Files (*.jpg)|*.jpg|GIF Files (*.gif)|*.gif"; 


    // Display OpenFileDialog by calling ShowDialog method 
    Nullable<bool> result = dlg.ShowDialog();


    // Get the selected file name and display in a TextBox 
    if (result == true)
    {
        // Open document 
        string filename = dlg.FileName;
        textBox1.Text = filename;
    }
}

