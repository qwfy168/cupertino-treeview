# Cupertino TreeView [![English](https://img.shields.io/badge/Language-English-blue.svg)](README.md) [![中文](https://img.shields.io/badge/Language-中文-red.svg)](README.zh-CN.md) [![한국어](https://img.shields.io/badge/Language-한국어-green.svg)](README.ko.md)

在WPF中实现的高级自定义TreeView控件，为复杂的层次结构数据提供现代化且灵活的解决方案

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![.NET](https://img.shields.io/badge/.NET-8.0-blue.svg)](https://dotnet.microsoft.com/download)
[![Stars](https://img.shields.io/github/stars/jamesnetgroup/cupertino-treeview.svg)](https://github.com/jamesnetgroup/cupertino-treeview/stargazers)
[![Issues](https://img.shields.io/github/issues/jamesnetgroup/cupertino-treeview.svg)](https://github.com/jamesnetgroup/cupertino-treeview/issues)

## 项目概述

Cupertino TreeView是一个高级CustomControl，重构并扩展了WPF的基本TreeView控件。利用继承自ItemsControl的独特结构，有效地表示复杂的层次数据，同时应用MVVM模式，提供出色的用户体验和开发人员友好的结构。

<img src="https://github.com/vickyqu115/cupertino-treeview/assets/101777355/b3f3aacd-6d96-4db9-b1d5-8bdd6cf3e2e0" width="100%"/>

## 主要特性和技术实现

#### 1. 高级CustomControl开发
- [x] 利用TreeView和TreeViewItem继承自ItemsControl的特殊层次结构
- [x] 将TreeView完全重构为CustomControl
- [x] 使用ToggleButton实现Expand功能

#### 2. MVVM模式集成
- [x] 通过ViewModel管理数据和业务逻辑
- [x] 使用ICommand DependencyProperty处理事件
- [x] 通过冒泡实现MVVM友好的TreeViewItem事件处理

#### 3. 应用高级WPF技术
- [x] 使用IValueConverter实现层次结构的可视化表示
- [x] 通过复杂的ItemsPresenter设计支持无限层次结构
- [x] 使用触发器和数据触发器实现动态UI更新

#### 4. 性能和用户体验优化
- [x] 应用UI虚拟化技术实现高效的项目渲染
- [x] MouseOver和IsSelected状态的精细可视化表现

#### 5. 文件系统建模
- [x] 创建模仿实际文件系统结构的演示数据
- [x] 通过递归算法处理深层文件夹结构

## 技术深度分析

- **TreeView和TreeViewItem的双重角色**：实现一个独特的结构，两个控件都继承自ItemsControl，同时扮演父级和子级角色
- **层次结构可视化**：使用DepthConverter自动计算每个项目基于深度的缩进
- **事件冒泡和MVVM**：实现一种模式，通过冒泡将TreeViewItem事件向上传播，并通过ICommand在ViewModel中处理
- **动态UI更新**：实现由IsExpanded、IsSelected等状态变化触发的UI更新
- **文件系统建模**：实现模仿实际文件系统结构的递归数据模型和生成逻辑

## 技术栈

- WPF (Windows Presentation Foundation)
- .NET 8.0
- C# 10.0
- XAML

## 入门指南

### 先决条件

- Visual Studio 2022 或更高版本
- .NET 8.0 SDK

### 安装和执行

#### 1. 克隆仓库：

```
git clone https://github.com/jamesnetgroup/cupertino-treeview.git
```

#### 2. 打开解决方案
- [x] Visual Studio
- [x] Visual Studio Code
- [x] JetBrains Rider

<img src="https://github.com/user-attachments/assets/af70f422-7057-4e77-a54d-042ee8358d2a" width="32%"/>
<img src="https://github.com/user-attachments/assets/e4feaa10-a107-4b58-8d13-1d8be620ec62" width="32%"/>
<img src="https://github.com/user-attachments/assets/5ff487f6-55e4-43e1-9abf-f8d419ee6943" width="32%"/>

#### 3. 构建和运行
- [x] 设置为启动项目
- [x] 按F5或点击运行按钮
- [x] 推荐使用Windows 11

## 学习资源

- [详细实现文章 (jamesnet.dev)](https://jamesnet.dev/article/112)
- [BiliBili 教程 (中文)](https://bit.ly/46AQp9Z)

## 贡献

欢迎对Cupertino TreeView做出贡献！请随时提交问题、创建拉取请求或提出改进建议。

## 许可证

本项目基于MIT许可证分发。有关详细信息，请参阅[LICENSE](LICENSE)文件。

## 联系方式

- 网站：https://jamesnet.dev
- 电子邮件：vickyqu115@hotmail.com, james@jamesnet.dev

使用Cupertino TreeView体验高级WPF控件开发和MVVM模式的实际应用！

------

## Why Customizing TreeView in WPF is Necessary

In WPF, TreeView and TreeViewItem provide default templates like other standard controls. However, TreeView offers diverse ways of representation and a free hierarchical layout without constraints, making the default templates somewhat limited. Therefore, it is crucial to thoroughly understand and utilize the mechanisms and characteristics of this TreeView control, which inherits from ItemsControl.

## TreeView Mechanism: Different from ListBox but Both Inherit ItemsControl

ListBox, one of the typical controls inheriting from ItemsControl, has a clear hierarchical mechanism between parent and child. Thus, while ListBox inherits from ItemsControl, ListBoxItem inherits from ContentControl, making the hierarchical structure intuitive to understand from the inheritance structure alone.

However, in the case of TreeView and TreeViewItem, the top-level parent is TreeView, but the child TreeViewItem can also contain its own children, acting as both parent and child. Hence, ironically, TreeViewItem also inherits from ItemsControl. This is a fundamental concept of the TreeView control.

## Understanding TreeView's Identity through ItemsSource Property and ItemsPresenter Element

As mentioned earlier, both TreeView and TreeViewItem inherit from ItemsControl, thus both controls have the ItemsSource collection property. Therefore, it is essential to specify the area for the ItemsPresenter element within the template for the parent control. Similarly, for recursive structures, the child control must also create a binding for the ItemsSource property and an area for the ItemsPresenter element.

The summarized source code is as follows:

_TreeView Template_
```xaml
<Style TargetType="{x:Type TreeView}">
    <Setter Property="ItemsSource" Value="{Binding Files}"/>
    <Setter Property="Template">
        <Setter.Value>
            <ControlTemplate>
                <ItemsPresenter/>
            </ControlTemplate>
        </Setter.Value>
    </Setter>
</Style>
```

_TreeViewItem Template_
```xaml
<Style TargetType="{x:Type TreeViewItem}">
    <Setter Property="ItemsSource" Value="{Binding Children}"/>
    <Setter Property="Template">
        <Setter.Value>
            <ControlTemplate>
                <StackPanel>
                    <TextBlock Text="{Binding Name}"/>
                    <ItemsPresenter/>
                </StackPanel>
            </ControlTemplate>
        </Setter.Value>
    </Setter>
</Style>
```

By comparing the two template source codes of TreeView and TreeViewItem, we can see the structural similarity where both use ItemsSource and ItemsPresenter. These mechanistic elements enable the TreeView control to expand freely and flexibly without any hierarchical constraints.

Therefore, understanding and configuring these features allows for the quick and easy implementation of a complex TreeView structure.

## Designing the Data Model for TreeView Control

First, you need to select data for hierarchical representation in the TreeView control. In this tutorial video, we use a folder/file structure as the basis for our data. This is an easily understandable example if you think of Windows Explorer or Mac Finder. It is also well-suited for representing recursive hierarchical structures.

The model design is as follows:

_FileItem Model_

```csharp
public class FileItem
{
    public string Name { get; set; }
    public string Path { get; set; }
    public string Type { get; set; }
    public string Extension { get; set; }
    public long? Size { get; set; }
    public int Depth { get; set; }
    public List<FileItem> Children { get; set; }
}
```

The model properties are the minimum required to represent Windows Explorer or Finder. The key properties to focus on are Path, Depth, and Children. Let's look at these properties in detail:

- Name: The name of the folder/file, extracted from Path.
- Path: The full path of the folder/file.
- Type: Distinguishes between folder and file.
- Extension: The file extension.
- Size: The size of the file.
- Depth: The depth (level) of the current item.
- Children: A list of child items.

## Creating Demo Data

Although you could load the actual system directories like Windows Explorer or Finder, for this tutorial, we prepare a safe execution by creating the folder/file structure in a common accessible space like My Documents.

Therefore, we need the following logic to create the folder/file structure:

_FileCreator.cs_

```csharp
public class FileCreator
{
    public string BasePath = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments);

    public void Create()
    {
        string textData = "Vicky test file content.";

        string[] tempFiles = 
        {
            @"\Vicky\Microsoft\Visual Studio\solution.txt",
            @"\Vicky\Microsoft\Visual Studio\debug.mp3",
            @"\Vicky\Microsoft\Visual Studio\class.cs",
            @"\Vicky\Microsoft\Sql Management Studio\query.txt",
            @"\Vicky\Apple\iPhone\store.txt",
            @"\Vicky\Apple\iPhone\calculator.mp3",
            @"\Vicky\Apple\iPhone\safari.cs",
        };

        foreach (string file in tempFiles)
        { 
            string fullPath = BasePath + file;
            string dirName = Path.GetDirectoryName(fullPath);

            if (!Directory.Exists(dirName))
            {
                Directory.CreateDirectory(dirName);
            }

            File.WriteAllText(fullPath, textData);
        }
    }
}
```

By examining the source code, you can see that the logic creates multiple folders and files based on the My Documents path (Environment.SpecialFolder.MyDocuments). Various items were created to form a hierarchical directory structure and include different file extensions. Feel free to create additional files as needed.

This creation logic ensures that the folders and files are safely generated within My Documents.

## MVVM Pattern

In this tutorial, we will set up the ViewModel for the MVVM pattern for the first time. The MVVM pattern is highly relied upon in WPF and plays a significant role.

However, we didn't cover it in the previous five tutorials because we intended to first provide a thorough understanding of the foundational elements of WPF, such as CustomControl, ControlTemplate, and ContentControl/ItemsControl, before introducing MVVM.

Therefore, if you want to strengthen your WPF foundation, we recommend studying the five WPF tutorial series in order before proceeding.

## Creating a List Based on Generated Folders/Files in the ViewModel

This tutorial introduces the core of the MVVM pattern: the ViewModel. We'll create a ViewModel class that uses the physical path defined in the FileCreator.cs class's BasePath. Using the .NET Directory class methods GetDirectories and GetFiles, we'll retrieve all folder/file lists and compose the FileItem data.

First, we create the List property to bind to the TreeView's ItemsSource.

_Files Property to Bind to ItemsSource_

```csharp
public List<FileItem> Files { get; set; }
```

It is notable that there is no OnPropertyChanged processing for the Files property. This implies that the Files list will be created in the ViewModel's constructor. Therefore, using `init` instead of `set` is also a good approach.

_Using init Instead_

```csharp
public List<FileItem> Files { get; init; }
```

Although a minor rule, such elements contribute to writing good code.

Next, we need to implement a method that recursively traverses folders and creates the folder/file list as FileItem models.


_Implementing GetFiles Method_

```csharp
private void GetFiles(string root, List<FileItem> source, int depth)
{
    string[] dirs = Directory.GetDirectories(root);
    string[] files = Directory.GetFiles(root);

    foreach (string dir in dirs)
    {
        FileItem item = new();
        item.Name = Path.GetFileNameWithoutExtension(dir);
        item.Path = dir;
        item.Size = null;
        item.Type = "Folder";
        item.Depth = depth;
        item.Children = new();

        source.Add(item);

        GetFiles(dir, item.Children, depth + 1);
    }

    foreach (string file in files)
    {
        FileItem item = new();
        item.Name = Path.GetFileNameWithoutExtension(file);
        item.Path = file;
        item.Size = new FileInfo(file).Length;
        item.Type = "File";
        item.Extension = new FileInfo(file).Extension;
        item.Depth = depth;

        source.Add(item);
    }
}
```

The first point to note in this source code is that the target folder/file items are recursively traversed only if they are directories. The recursive calls occur within the `foreach` loop for `dirs`, where children are continuously added through the `Children` property.

Next is the Depth property. This property pre-calculates how many levels deep the current folder/file is. While the data is logically hierarchical and can be distinguished in XAML during the design process of the TreeViewItem Template, it is essential to know the item's level visually. Therefore, each time the recursive method is called, the Depth value increases to differentiate the hierarchy. Other elements are primarily for visual data representation, so they can be reviewed briefly.

## Reviewing the Complete ViewModel Code

Now, let's review the complete ViewModel code to see how the Files property is created at the constructor stage.

_CupertinoViewModel.cs_

```csharp
public partial class CupertinoWindowViewModel : ObservableBase
{
    public List<FileItem> Files { get; set; }
    public CupertinoWindowViewModel()
    {
        FileCreator fileCreator = new();
        fileCreator.Create();

        int depth = 0;
        string root = fileCreator.BasePath + "/Vicky";
        List<FileItem> source = new();

        GetFiles(root, source, depth);

        Files = source;
    }

    private void GetFiles(string root, List<FileItem> source, int depth)
    {
        string[] dirs = Directory.GetDirectories(root);
        string[] files = Directory.GetFiles(root);

        foreach (string dir in dirs)
        {
            FileItem item = new();
            item.Name = Path.GetFileNameWithoutExtension(dir);
            item.Path = dir;
            item.Size = null;
            item.Type = "Folder";
            item.Depth = depth;
            item.Children = new();

            source.Add(item);

            GetFiles(dir, item.Children, depth + 1);
        }

        foreach (string file in files)
        {
            FileItem item = new();
            item.Name = Path.GetFileNameWithoutExtension(file);
            item.Path = file;
            item.Size = new FileInfo(file).Length;
            item.Type = "File";
            item.Extension = new FileInfo(file).Extension;
            item.Depth = depth;

            source.Add(item);
        }
    }
}
```

By examining the source code, you can see that all the preliminary work for structuring the data is implemented in the constructor.

The constructor handles setting the binding properties before the ViewModel is bound to the Window's DataContext. While it is preferable to load large amounts of data asynchronously, in this tutorial, we handle it within the constructor due to the small data size for constructing the TreeView. Understanding and using these characteristics will help you implement MVVM-based WPF applications more effectively.

Now, let's delve into the part where the Files property is defined in the ViewModel's constructor.

_Constructor_

```csharp
FileCreator fileCreator = new();
fileCreator.Create();

int depth = 0;
string root = fileCreator.BasePath + "/Vicky";
List<FileItem> source = new();

GetFiles(root, source, depth);

Files = source;
```
The logic included in the constructor is as follows:

- `fileCreator.Create`: Generates sample demo data in the My Documents path.
- `depth`: Initializes the depth of the first folder/file item to 0.
- `root`: Base folder in the My Documents path (you can configure another folder here).
- `source`: Creates a new list.
- `GetFiles`: Starts recursive traversal of folders/files based on the root My Documents path.
- `Files = source`: Assigns the source to Files after the recursive calls are completed.

This completes all preparations for data configuration and TreeView ItemsSource data binding through the ViewModel (MVVM pattern).

## DataContext Binding

In this Cupertino Treeview tutorial, we don't use MVVM-related framework features like Prism. Instead, we directly bind the ViewModel in the window's constructor as follows:

```csharp
namespace Cupertino.Forms.UI.Views
{
    public class CupertinoWindow : Window
    {
        static CupertinoWindow()
        {
            DefaultStyleKeyProperty.OverrideMetadata(typeof(CupertinoWindow), 
                new FrameworkPropertyMetadata(typeof(CupertinoWindow)));
        }

        public CupertinoWindow()
        {
            DataContext = new CupertinoWindowViewModel();
        }
    }
}
```

If the data is not bound when running, check this part where the ViewModel is bound to the DataContext.

Now, the major preparations in the code-behind are complete.

## Cupertino TreeView ControlTemplate

Implementing the TreeView ControlTemplate is very similar to implementing a ListBox. The most important element is the ItemsPresenter. When adding layout elements like headers or pagination, this is where you implement them. In this tutorial, we include a header, so the ItemsPresenter and header are implemented within the TreeView Template.

Below is the complete implementation of the CupertinoTreeView CustomControl Template.

_CupertinoTreeView.xaml_

```xaml
<Style TargetType="{x:Type units:CupertinoTreeView}">
    <Setter Property="Width" Value="800"/>
    <Setter Property="BorderBrush" Value="#AAAAAA"/>
    <Setter Property="BorderThickness" Value="1"/>
    <Setter Property="Margin" Value="100"/>
    <Setter Property="Template">
        <Setter.Value>
            <ControlTemplate TargetType="{x:Type units:CupertinoTreeView}">
                <Border Background="{TemplateBinding Background}"
                        BorderBrush="{TemplateBinding BorderBrush}"
                        BorderThickness="{TemplateBinding BorderThickness}">
                    <Grid Grid.IsSharedSizeScope="True">
                        <Grid.RowDefinitions>
                            <RowDefinition Height="Auto"/>
                            <RowDefinition Height="*"/>
                        </Grid.RowDefinitions>
                        <Grid.ColumnDefinitions>
                            <ColumnDefinition Width="*"/>
                            <ColumnDefinition Width="Auto" MinWidth="400" SharedSizeGroup="Path"/>
                            <ColumnDefinition Width="Auto" MinWidth="100" SharedSizeGroup="Size"/>
                        </Grid.ColumnDefinitions>
                        <Label Grid.Column="0" Content="Name" 
                               Background="#FAFAFA" Padding="10" 
                               BorderBrush="#AAAAAA" BorderThickness="0 0 1 1"/>
                        <Label Grid.Column="1" Content="Path" 
                               Background="#FAFAFA" Padding="10" 
                               BorderBrush="#AAAAAA" BorderThickness="0 0 1 1"/>
                        <Label Grid.Column="2" Content="Size" 
                               Background="#FAFAFA" Padding="10" 
                               BorderBrush="#AAAAAA" BorderThickness="0 0 1 1"/>
                        <units:MagicStackPanel Grid.Row="1" Grid.ColumnSpan="3" 
                            VerticalAlignment="Top"
                            ItemHeight="{Binding ElementName=Items, Path=ActualHeight}">
                        </units:MagicStackPanel>
                        <ItemsPresenter x:Name="Items" Grid.Row="1" Grid.ColumnSpan="3" 
                                        VerticalAlignment="Top"/>
                    </Grid>
                </Border>
            </ControlTemplate>
        </Setter.Value>
    </Setter>
</Style>
```

The key points here are the configuration of the header and the placement of the ItemsPresenter element. The TreeView control does not inherently provide elements like headers. From a user interface perspective, it is uncommon to display headers in a TreeView. However, if needed, you can implement a header directly as shown here.

_Header Positioned Above ItemsPresenter_



To ensure that the column sizes of TreeViewItem data items generated in the header and ItemsPresenter are consistent, we use the SharedSizeGroup property (Path, Size). These elements will also appear later in the TreeViewItem content.

In conclusion, configuring the header and placing the ItemsPresenter for child elements is crucial in implementing the TreeView control's Template. This is relatively simpler compared to implementing TreeViewItem.

## Cupertino TreeViewItem ControlTemplate

Finally, we come to the most important core element of the TreeView control: implementing the TreeViewItem Template.

As mentioned earlier, a TreeViewItem, despite being a child, also acts as a parent, inheriting from ItemsControl. Therefore, its Template needs to include an ItemsPresenter for its children, similar to ListBoxItem but accommodating a hierarchical structure.

Although it may seem complex, the layout can be simplified as follows:

```xaml
<Border>
    <StackPanel>
        <!-- Content such as file name, file size -->
        <Grid>
        </Grid>
        <!-- Child elements -->
        <ItemsPresenter/>
    </StackPanel>
</Border>
```

The TreeViewItem Template must properly place not only the content but also the ItemsPresenter element. This ensures that when hierarchical data is bound to ItemsSource, the TreeView is correctly structured.

If you implement the TreeView control without properly understanding the unique mechanism of TreeViewItem, it can be relatively challenging.

> This tutorial video focuses on thoroughly understanding the concept of the TreeView control, offering over an hour of detailed content. Repeated practice will be beneficial.

Below is the complete implementation of the TreeViewItem Template.

_CupertinoTreeItem.xaml_

```xaml
<Style TargetType="{x:Type units:CupertinoTreeItem}">
    <Setter Property="SelectionCommand" Value="{Binding RelativeSource={RelativeSource AncestorType=units:CupertinoTreeView}, Path=DataContext.SelectionCommand}"/>
    <Setter Property="Background" Value="Transparent"/>
    <Setter Property="ItemsSource" Value="{Binding Children}"/>
    <Setter Property="Template">
        <Setter.Value>
            <ControlTemplate TargetType="{x:Type units:CupertinoTreeItem}">
                <Border Background="{TemplateBinding Background}"
                        BorderBrush="{TemplateBinding BorderBrush}"
                        BorderThickness="{TemplateBinding BorderThickness}">
                    <StackPanel>
                        <Grid x:Name="Item" Background="{TemplateBinding Background}" Height="36">
                            <Grid.ColumnDefinitions>
                                <ColumnDefinition Width="*"/>
                                <ColumnDefinition Width="Auto" MinWidth="200" SharedSizeGroup="Path"/>
                                <ColumnDefinition Width="Auto" MinWidth="100" SharedSizeGroup="Size"/>
                            </Grid.ColumnDefinitions>
                            <StackPanel Orientation="Horizontal" Margin="{Binding Depth, Converter={cnvts:DepthConverter}}">
                                <units:ChevronSwitch x:Name="Chevron" Margin="10" IsChecked="{Binding RelativeSource={RelativeSource Templatedparent}, Path=IsExpanded}"/>
                                <units:FileIcon Type="{Binding Type}" Margin="10" Extension="{Binding Extension}"/>
                                <TextBlock Text="{Binding Name}" Margin="10"/>
                            </StackPanel>
                            <TextBlock Grid.Column="1" Text="{Binding Path}" Margin="10"/>
                            <TextBlock Grid.Column="2" Text="{Binding Size, Converter={cnvts:SizeConverter}}" Margin="10"/>
                        </Grid>

                        <ItemsPresenter x:Name="Items" Visibility="Collapsed"/>
                    </StackPanel>
                </Border>
                <ControlTemplate.Triggers>
                    <Trigger Property="IsExpanded" Value="True">
                        <Setter TargetName="Items" Property="Visibility" Value="Visible"/>
                    </Trigger>
                    <DataTrigger Binding="{Binding ElementName=Item, Path=IsMouseOver}" Value="True">
                        <Setter TargetName="Item" Property="Background" Value="#D1E3FF"/>
                    </DataTrigger>
                    <Trigger Property="IsSelected" Value="True">
                        <Setter TargetName="Item" Property="Background" Value="#004EFF"/>
                        <Setter TargetName="Item" Property="TextBlock.Foreground" Value="#FFFFFF"/>
                    </Trigger>
                    <DataTrigger Binding="{Binding Type}" Value="File">
                        <Setter TargetName="Chevron" Property="Visibility" Value="Hidden"/>
                    </DataTrigger>
                </ControlTemplate.Triggers>
            </ControlTemplate>
        </Setter.Value>
    </Setter>
</Style>
```

This implementation includes displaying the file name, path, file size, extension icon, and the ItemsPresenter for placing child elements.

Next, check the generated path to ensure the actual directory matches within My Documents.

![CupertinoPNG2](https://github.com/vickyqu115/cupertino-treeview/assets/101777355/dfd5cdd1-650b-4314-8756-3693f5d743a1)


## Design Elements

No special design elements were used in this tutorial. A simple combination of Border's Background/BorderBrush colors and layout design elements like Margin/Padding can produce excellent results.

The key is consistent Margin and Padding for all visual elements. Repeated adjustments are necessary to achieve a visually appealing control. Valuing this practice will enhance your visual design skills.

## Depth Converter

Since the depth of all file items has already been calculated, we can convert this depth into a left margin for each item to visually represent the parent-child hierarchy. By utilizing the Depth value in TreeView, you can set a left margin proportional to the Depth, clearly displaying the hierarchical relationships between items.

Here is the DepthConverter inheriting from IValueConverter.

_DepthConverter.cs_

```csharp
public class DepthConverter : MarkupExtension, IValueConverter
{
    public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
    {
        int depth = (int)value;
        Thickness margin = new Thickness(depth * 20, 0, 0, 0);
        return margin;
    }

    public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
    {
        throw new NotImplementedException();
    }

    public override object ProvideValue(IServiceProvider serviceProvider)
    {
        return this;
    }
}
```

This code includes logic to convert the Depth value to a Thickness structure for calculating the left margin. It also inherits from MarkupExtension for easier use in XAML.

_Using DepthConverter_

```xaml
<StackPanel Orientation="Horizontal" Margin="{Binding Depth, Converter={local:DepthConverter}}">
```

The final result, with the Depth value applied as a left margin, can be seen in the image below.

_Depth Applied as Left Margin_

![CupertinoPGNG3](https://github.com/vickyqu115/cupertino-treeview/assets/101777355/d9a2e99e-3202-49df-a630-b3e4a3f78d52)

The image clearly shows how the Depth value is applied, using a red dividing line for clarity. Experiment with changing the `depth * 20` value in the DepthConverter logic to see the effects.

## Conclusion

Although not covered in this article, the tutorial video explains the Depth concept in detail using animations. It also includes methods for handling selected TreeView items using ICommand in the ViewModel and solving issues related to event bubbling.

The tutorial video is over an hour long, packed with detailed and in-depth content. You can watch it with English narration on YouTube and Chinese narration on Bilibili. Please support by subscribing, liking, and sharing the video to help more developers. The source code is shared as open-source on [GitHub](https://github.com/jamesnetgroup/cupertino-treeview), and we welcome your support through Stars, Forks, and Discussions.

Thank you.
