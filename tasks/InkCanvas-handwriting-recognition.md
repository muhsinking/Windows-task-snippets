# Ink handwriting recogniztion
Creates an Ink Canvas and a button, which can be pressed to recognize handwritten text on the canvas. Another button is added to clear handwriting from the canvas.

## XAML
```xml
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
  <InkCanvas Name="ink"></InkCanvas>
  <StackPanel>
    <TextBlock Name="resultBlock" Margin="20"/>
    <Button Content="Recognize text" Click="RecognizeText" Margin="20"/> 
    <Button Content="Clear canvas" Click="ClearCanvas" Margin="20"/>
  </StackPanel>
</Grid> 
```

## C# #

```CSharp
public MainPage()
{
  this.InitializeComponent();
  inkRecognizerContainer = new InkRecognizerContainer();
  ink.InkPresenter.InputDeviceTypes = Windows.UI.Core.CoreInputDeviceTypes.Mouse | Windows.UI.Core.CoreInputDeviceTypes.Touch | Windows.UI.Core.CoreInputDeviceTypes.Pen;
}

async void RecognizeText(object sender RoutedEventArgs e){
  var result = await inkRecognizerContainer.RecognizeAsync(ink.InkPresenter.StrokeContainer, InkRecognitionTarget.All);
  string s = result[0].GetTextCandidates()[0];
  resultBlock.Text = s;
}

void ClearCanvas(object sender, RoutedEventArgs e)
{
  ink.InkPresenter.StrokeContainer.Clear();
  resultBlock.Text = "";
}
```
