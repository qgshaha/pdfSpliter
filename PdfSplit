
using PdfSharpCore.Pdf;
using PdfSharpCore.Pdf.IO;
using System.Collections.Generic;
using System.IO;
using System.Text;

namespace WinPdfReader
{
    public class PdfSplit
    {
        public static Dictionary<string, int> Split(string filePath, ref StringBuilder sb)
        {
            var filePathList = new Dictionary<string, int>();

            // 创建输出文件所在文件夹
            string outputFolder = "splited";
            string rootPath = Directory.GetCurrentDirectory();
            string folderAll = Path.Combine(rootPath, outputFolder);
            if (!Directory.Exists(folderAll))
            {
                Directory.CreateDirectory(folderAll);
            }
            var newFileNamePrefix = Path.GetFileNameWithoutExtension(filePath);

            // Get a fresh copy of the sample PDF file
            string filename = filePath;
            //File.Copy(Path.Combine("../../../../../PDFs/", filename),
            //Path.Combine(Directory.GetCurrentDirectory(), filename), true);

            // Open the file
            PdfDocument inputDocument = PdfReader.Open(filename, PdfDocumentOpenMode.Import);

            string name = Path.GetFileNameWithoutExtension(filename);
            for (int idx = 0; idx < inputDocument.PageCount; idx++)
            {
                // Create new document
                PdfDocument outputDocument = new PdfDocument();
                outputDocument.Version = inputDocument.Version;
                outputDocument.Info.Title = string.Format("Page {0} of {1}", idx + 1, inputDocument.Info.Title);
                outputDocument.Info.Creator = inputDocument.Info.Creator;


                string newFilePath = Path.Combine(outputFolder, $"{newFileNamePrefix}_size_{idx + 1}_{idx + 1}.pdf");
                // Add the page and save it
                outputDocument.AddPage(inputDocument.Pages[idx]);
                outputDocument.Save(newFilePath);
                filePathList.Add(newFilePath, 1);
                sb.AppendLine($"splited file: {newFilePath}");
            }

            return filePathList;
        }
    }
}
