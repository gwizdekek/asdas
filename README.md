using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IO;
using System.Security;
using System.Windows.Forms;

namespace _22._09._21
{
public partial class Form1 : Form
{
public Form1()
{
InitializeComponent();
}

private void openFileDialog1_FileOk(object sender, CancelEventArgs e)
{

}

private void button1_Click(object sender, EventArgs e)
{
Stream myStream = null;
OpenFileDialog theDialog = new OpenFileDialog();
theDialog.Title = "Open Text File";
theDialog.Filter = "All files[*.*]TXT files|*.txt";
theDialog.FilterIndex = 2;
theDialog.InitialDirectory = @"C;\";
if (theDialog.ShowDialog() == DialogResult.OK)
{
try
{
if ((myStream = theDialog.OpenFile()) != null)
{
using (var reader = new StreamReader(theDialog.FileName))
{
string line;
while ((line = reader.ReadLine()) != null)
{
textBox1.Text += line;
textBox1.AppendText(Environment.NewLine);
}
}
}
}
catch { }

}
}

private void button2_Click(object sender, EventArgs e)
{
using (var saveFileDialog = new SaveFileDialog())
{

saveFileDialog.Filter = "txt files (*.txt)|*.txt|All files (*.*)|*.*";
saveFileDialog.FilterIndex = 2;

try
{
if (saveFileDialog.ShowDialog() == DialogResult.OK)
{
File.WriteAllText(saveFileDialog.FileName, textBox1.Text);
}
}
catch (Exception ex)
{
MessageBox.Show("Error: Could not save file to disk. Original error:" + ex.Message);
}
}
}

private void textBox1_TextChanged(object sender, EventArgs e)
{

}

}
}
