# BasicRegistrationForm
using System.Data.SqlClient;
using Microsoft.Data.SqlClient;
using Microsoft.Win32;

namespace RegistrationForm
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            SqlConnection con = new SqlConnection("Data Source=MOBIN-PC\\SQLEXPRESS;Initial Catalog=RegistrationForm;Integrated Security=True;Trust Server Certificate=True");
            con.Open();
            string insertQuery = "insert into register values (@Firstname,@Lastname,@Gender,@Email,@Username,@Password)";
            SqlCommand cmd = new SqlCommand(insertQuery, con);
            cmd.Parameters.AddWithValue("@Firstname", this.textBox1.Text);
            cmd.Parameters.AddWithValue("@Lastname", this.textBox2.Text);
            cmd.Parameters.AddWithValue("@Gender", this.comboBox1.Text);
            cmd.Parameters.AddWithValue("@Email", this.textBox4.Text);
            cmd.Parameters.AddWithValue("@Username", this.textBox5.Text);
            cmd.Parameters.AddWithValue("@Password", this.textBox6.Text);
            cmd.ExecuteNonQuery();
            MessageBox.Show("registeration success");
            this.Close();

        }


        private void button2_Click(object sender, EventArgs e)
        {
            SqlConnection conn = new SqlConnection("Data Source=MOBIN-PC\\SQLEXPRESS;Initial Catalog=RegistrationForm;Integrated Security=True;Trust Server Certificate=True");
            conn.Open();
            string query = "Select * from Register where username =@Username AND Password = @Password";
            SqlCommand cmd = new SqlCommand(query,conn);
            cmd.Parameters.AddWithValue("@Username",this.textBox5.Text);
            cmd.Parameters.AddWithValue("@Password",this.textBox6.Text);
            //int count = (Convert.ToInt32((int)cmd.ExecuteScalar())); // Get the number of matching records

            //if (count > 0)
            //{
            //   
            //}
            //else
            //{
            //    MessageBox.Show("Invalid username or password");
            //}
            MessageBox.Show("Login success");
            this.Close();   
           
        }

        private void button3_Click(object sender, EventArgs e)
        {
            this.Close();
        }

        private void textBox6_TextChanged(object sender, EventArgs e)
        {
            textBox1.PasswordChar = '*';
        }
    }
}
