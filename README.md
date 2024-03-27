- 👋 Hi, I’m @STEVEINK
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace ProductManagementApp
{
    public partial class MainForm : Form
    {
        private List<Product> products = new List<Product>();

        public MainForm()
        {
            InitializeComponent();

            // Adiciona colunas à listagem
            listViewProducts.Columns.Add("Nome", 150);
            listViewProducts.Columns.Add("Valor", 100);

            // Ordenação inicial por valor do menor para o maior
            listViewProducts.ListViewItemSorter = new ListViewItemComparer(1);

            // Atualiza a listagem
            UpdateProductList();
        }

        private void UpdateProductList()
        {
            listViewProducts.Items.Clear();
            foreach (var product in products)
            {
                string[] row = { product.Name, product.Value.ToString("C2") };
                var listViewItem = new ListViewItem(row);
                listViewProducts.Items.Add(listViewItem);
            }
        }

        private void btnAddProduct_Click(object sender, EventArgs e)
        {
            // Cria e exibe o formulário de adição de produto
            var addProductForm = new AddProductForm();
            if (addProductForm.ShowDialog() == DialogResult.OK)
            {
                products.Add(addProductForm.Product);
                UpdateProductList();
            }
        }

        // Classe para comparar itens na listagem para ordenação
        public class ListViewItemComparer : IComparer
        {
            private int column;

            public ListViewItemComparer(int column)
            {
                this.column = column;
            }

            public int Compare(object x, object y)
            {
                return decimal.Compare(
                    decimal.Parse(((ListViewItem)x).SubItems[column].Text, System.Globalization.NumberStyles.Currency),
                    decimal.Parse(((ListViewItem)y).SubItems[column].Text, System.Globalization.NumberStyles.Currency)
                );
            }
        }
    }

    public class Product
    {
        public string Name { get; set; }
        public string Description { get; set; }
        public decimal Value { get; set; }
        public bool AvailableForSale { get; set; }
    }
}
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
STEVEINK/STEVEINK is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
