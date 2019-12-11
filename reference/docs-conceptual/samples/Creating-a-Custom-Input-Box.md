---
ms.date: 06/05/2017
keywords: powershell,cmdlet
title: 创建自定义输入框
ms.openlocfilehash: 9c1c3c72482157e849c0259e7d2e25ed969a4aab
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "67030225"
---
# <a name="creating-a-custom-input-box"></a>创建自定义输入框

通过使用 Windows PowerShell 3.0 及更高版本中的 Microsoft .NET Framework 窗体构建功能为图形自定义输入框编写脚本。

## <a name="create-a-custom-graphical-input-box"></a>创建自定义图形输入框

复制以下内容并将其粘贴到 Windows PowerShell ISE 中，然后将其另存为 Windows PowerShell 脚本 (.ps1)。

```powershell
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

$form = New-Object System.Windows.Forms.Form
$form.Text = 'Data Entry Form'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'

$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)

$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)

$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please enter the information in the space below:'
$form.Controls.Add($label)

$textBox = New-Object System.Windows.Forms.TextBox
$textBox.Location = New-Object System.Drawing.Point(10,40)
$textBox.Size = New-Object System.Drawing.Size(260,20)
$form.Controls.Add($textBox)

$form.Topmost = $true

$form.Add_Shown({$textBox.Select()})
$result = $form.ShowDialog()

if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $textBox.Text
    $x
}
```

该脚本首先加载两个 .NET Framework 类：System.Drawing 和 System.Windows.Forms   。 然后，启动 .NET Framework 类 **System.Windows.Forms.Form** 的新实例；它提供一个可以开始添加控件的空白窗体或窗口。

```powershell
$form = New-Object System.Windows.Forms.Form
```

在创建 Form 类的实例后，为此类的三个属性赋值。

- **文本。** 这将成为该窗口的标题。

- **大小。** 这是窗体的大小（以像素为单位）。 上述脚本创建的窗体大小为宽 300 像素、高 200 像素。

- **StartingPosition。** 在上述脚本中，此可选属性将设置为 **CenterScreen**。 如果未添加此属性，Windows 将在窗体打开时选择一个位置。 通过将 **StartingPosition** 设置为 **CenterScreen**，可使窗体在每次加载时都自动显示在屏幕中间。

```powershell
$form.Text = 'Data Entry Form'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'
```

接下来，为窗体创建“确定”按钮。  指定“确定”按钮的大小和行为。  在此示例中，按钮位置为距窗体上边缘 120 像素，距左边缘 75 像素。 按钮高度为 23 像素，按钮长度为 75 像素。 此脚本使用预定义的 Windows 窗体类型确定按钮行为。

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

采用相同方式创建“取消”按钮。  “取消”按钮距窗口上边缘 120 像素，但距左边缘 150 像素。 

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

接下来，在窗口上提供标签文本，用于描述你希望用户提供的信息。

```powershell
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please enter the information in the space below:'
$form.Controls.Add($label)
```

添加控件（在本例中为文本框），从而让用户提供你在标签文本中描述的信息。 除了文本框，你还可以应用许多其他控件；有关更多控件，请参阅 MSDN 上的 [System.Windows.Forms 命名空间](https://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx)。

```powershell
$textBox = New-Object System.Windows.Forms.TextBox
$textBox.Location = New-Object System.Drawing.Point(10,40)
$textBox.Size = New-Object System.Drawing.Size(260,20)
$form.Controls.Add($textBox)
```

将 Topmost  属性设置为 $True  ，以强制此窗口在其他已打开的窗口和对话框之上打开。

```powershell
$form.Topmost = $true
```

接下来，添加此代码行以激活窗体，并将焦点设置到你创建的文本框。

```powershell
$form.Add_Shown({$textBox.Select()})
```

添加以下代码行以在 Windows 中显示该窗体。

```powershell
$result = $form.ShowDialog()
```

最后，**If** 块内的代码指示在用户在文本框中提供文本，然后单击“确定”按钮或按“Enter”键后，Windows 应如何处理该窗体。  

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $textBox.Text
    $x
}
```

## <a name="see-also"></a>另请参阅

- [你好，脚本专家：为什么这些 PowerShell GUI 示例不起作用呢？](https://go.microsoft.com/fwlink/?LinkId=506644)
- [GitHub：Dave Wyatt 的 WinFormsExampleUpdates](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [本周 Windows PowerShell 提示：创建自定义输入框](https://technet.microsoft.com/library/ff730941.aspx)
