NotePad
=
# 基本功能</br>
## 显示创建时间</br>
  1. 演示结果</br>
  ![显示创建时间](https://github.com/zishudanhuangsu/T/blob/master/q1.png)</br>
  2. 代码实现</br>
  * noteslist_item.xml</br>
  添加显示时间的TextView
  ```
  <TextView</br>
        android:id="@+id/text1_time"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:textAppearance="?android:attr/textAppearanceSmall"
        android:paddingLeft="5dip"
        android:textColor="@color/colorBlack"/>
   ```
   * NoteList.java</br>
   ```
    private static final String[] PROJECTION = new String[] {
            NotePad.Notes._ID, 
            NotePad.Notes.COLUMN_NAME_TITLE, 
            NotePad.Notes.COLUMN_NAME_CREATE_DATE,      
    };
   ```
   ```
   String[] dataColumns = { NotePad.Notes.COLUMN_NAME_TITLE ,  NotePad.Notes.COLUMN_NAME_CREATE_DATE } ;
   int[] viewIDs = { android.R.id.text1 , R.id.text1_time };
   ```
## 搜索功能</br>
  1. 演示结果</br>
  ![搜索功能](https://github.com/zishudanhuangsu/T/blob/master/q3.png)</br>
  2. 代码实现</br>
  * note_search_list.xml</br>
  ```
  <?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent">
    <SearchView
        android:id="@+id/search_view"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:iconifiedByDefault="false"
        android:queryHint="输入搜索内容..."
        android:layout_alignParentTop="true">
    </SearchView>
    <ListView
        android:id="@android:id/list"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">
    </ListView>
</LinearLayout>
  ```
  * NoteSearch</br>
  ```
 private static final String[] PROJECTION = new String[] {
            NotePad.Notes._ID, 
            NotePad.Notes.COLUMN_NAME_TITLE, 
            NotePad.Notes.COLUMN_NAME_CREATE_DATE, 
    };
  ```
  ```
  public boolean onQueryTextChange(String newText) {
        String selection = NotePad.Notes.COLUMN_NAME_TITLE + " Like ? ";
        String[] selectionArgs = { "%"+newText+"%" };
        Cursor cursor = managedQuery(
                getIntent().getData(),            
                PROJECTION,                       
                selection,                        
                selectionArgs,                    
                NotePad.Notes.DEFAULT_SORT_ORDER  
        );
        String[] dataColumns = { NotePad.Notes.COLUMN_NAME_TITLE ,  NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE };
        int[] viewIDs = { android.R.id.text1 , R.id.text1_time };
        MyCursorAdapter adapter = new MyCursorAdapter(
                this,
                R.layout.noteslist_item,
                cursor,
                dataColumns,
                viewIDs
        );
        setListAdapter(adapter);
        return true;
    }
  ```
# 扩展功能</br>
## UI美化</br>
  1. UI美化</br>
  修改笔记背景</br>
  ![UI](https://github.com/zishudanhuangsu/T/blob/master/q2.png)</br>

