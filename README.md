# new-SQLite-test01
package com.example.administrator.myfirstapplication;

import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.util.Log;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
//      创建一个数据库 并打开
        SQLiteDatabase db =openOrCreateDatabase("user.db",MODE_PRIVATE,null);
            db.execSQL("create table if not exists usertb(_id integer primary key autoincrement,name text not null,age integer not null,sex text not null)");
            db.execSQL("insert into usertb(name,sex,age) values('小明','男',18)");
            db.execSQL("insert into usertb(name,sex,age) values('小强','男',20)");
            db.execSQL("insert into usertb(name,sex,age) values('小丽','女',19)");
            db.execSQL("insert into usertb(name,sex,age) values('小华','男',19)");

            Cursor c= db.rawQuery("slect * from usertb",null);
                if (c !=null)
                {
                    while (c.moveToNext())
                    {
                        Log.i("info","_id:"+ c.getInt(c.getColumnIndex("_id" )));
                        Log.i("info","name:"+ c.getString(c.getColumnIndex("name")));
                        Log.i("info","age"+ c.getInt(c.getColumnIndex("age" )));
                        Log.i("info","sex"+ c.getString(c.getColumnIndex("sex")));
                        Log.i("info","################################");

                    }
                    c.close();
                }
                db.close();


    }
}
