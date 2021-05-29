/*************************************************************************************

   Toolkit for WPF

   Copyright (C) 2007-2017 Xceed Software Inc.

   This program is provided to you under the terms of the Microsoft Public
   License (Ms-PL) as published at http://wpftoolkit.codeplex.com/license 

   For more features, controls, and fast professional support,
   pick up the Plus Edition at https://xceed.com/xceed-toolkit-plus-for-wpf/

   Stay informed: follow @datagrid on Twitter or Like http://facebook.com/datagrids

  ************************************************************************************/

using System.Windows;
using Xceed.Wpf.AvalonDock.Layout.Serialization;
using System.IO;
using System;

namespace Xceed.Wpf.Toolkit.LiveExplorer.Samples.AvalonDock.Views
{
  /// <summary>
  /// Interaction logic for AvalonDockView.xaml
  /// </summary>
  public partial class AvalonDockView : DemoView
  {
    public AvalonDockView()
    {
      InitializeComponent();
    }

    private void SaveButton_Click( object sender, RoutedEventArgs e )
    {
        MessageBox.Show("EncDocumentPane.SelectedContentIndex = " + EncDocumentPane.SelectedContentIndex.ToString());
      using( var writer = new StreamWriter( "AvalonDockSavedFile.txt" ) )
      {
        var layoutSerializer = new XmlLayoutSerializer( _dockingManager );
        layoutSerializer.Serialize( writer );
      }
    }

    private void LoadButton_Click( object sender, RoutedEventArgs e )
    {
      using( var reader = new StreamReader( "AvalonDockSavedFile.txt" ) )
      {
        var layoutSerializer = new XmlLayoutSerializer( _dockingManager );
        layoutSerializer.Deserialize( reader );
      }
    }
 
    private void EncDocumentPane_PropertyChanged(object sender, System.ComponentModel.PropertyChangedEventArgs e)
    { 
        //MessageBox.Show(e.PropertyName);
    }

    private void EncDocumentPane_MouseDown(object sender, System.Windows.Input.MouseButtonEventArgs e)
    {
        MainWindow.m_bCanDragMove = false;
    }

    private void EncDocumentPane_MouseUp(object sender, System.Windows.Input.MouseButtonEventArgs e)
    {
        MainWindow.m_bCanDragMove = true;

    }

    private void EncDocument_IsSelectedChanged(object sender, EventArgs e)
    {
        if (EncDocumentPane.SelectedContentIndex == -1)
        {
            return;
        }
        if (EncDocumentPane.Children.Count == 2)
        {
            Console.WriteLine("EncDocumentPane.SelectedContentIndex = " + EncDocumentPane.SelectedContentIndex.ToString());
            Console.WriteLine("SelectedContent index = " + EncDocumentPane.IndexOf(EncDocumentPane.SelectedContent).ToString());
            if (EncDocumentPane.SelectedContent.ContentId != "ID_ENC_MAP")
            {
                //m_EncWin.Hide();
            }
            else
            {
                // m_EncWin.Show();
            }
        }
        else
        {
            // m_EncWin.Show();
        }

    }

    private void EncDocument_IsActiveChanged(object sender, EventArgs e)
    {
        if (EncDocumentPane.SelectedContentIndex == -1)
        {
            return;
        }
        if (EncDocumentPane.Children.Count == 2)
        {
            Console.WriteLine("EncDocumentPane.SelectedContentIndex = " + EncDocumentPane.SelectedContentIndex.ToString());
            Console.WriteLine("SelectedContent index = " + EncDocumentPane.IndexOf(EncDocumentPane.SelectedContent).ToString());
            if (EncDocumentPane.SelectedContent.ContentId != "ID_ENC_MAP")
            {
                //m_EncWin.Hide();
            }
            else
            {
                // m_EncWin.Show();
            }
        }
        else
        {
            // m_EncWin.Show();
        }
    }
  }
}
