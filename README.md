package com.example.code06;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Context;
import android.content.res.TypedArray;
import android.os.Bundle;
import android.widget.ArrayAdapter;
import android.widget.ListView;
import android.widget.SimpleAdapter;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public abstract class MainActivity extends AppCompatActivity {
    private String[] titles = null;
    private String[] authors = null;

    private static final String NEWS_TITLE = "nes_title";
    private static final String NEWS_AUTHOR = "news_author";

    private List<Map<String,String>> dataList = new ArrayList<>();

    public static final String NEWS_ID ="news_id";
    private List<News>newsList = new ArrayList<>();
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        titles = getResources().getStringArray(R.array.titles);
        authors = getResources().getStringArray(R.array.authors);

        ArrayAdapter<String>adapter = new ArrayAdapter<String>(
                MainActivity.this,android.R.layout.simple_list_item_1,titles
        );

        ListView lvNewslist = findViewById(R.id.Lv_news_List);
        lvNewslist.setAdapter(adapter);

        initData();

        SimpleAdapter simpleAdapter = new SimpleAdapter(MainActivity.this,
                dataList,android.R.layout.simple_list_item_2,
                new String[]{NEWS_TITLE,NEWS_AUTHOR},
                new int[]{android.R.id.text1,android.R.id.text2});

        ListView lvNewsList = findViewById(R.id.Lv_news_List);
        lvNewsList.setAdapter(simpleAdapter);
    }




    private void initData() {
        int length;
        titles = getResources().getStringArray(R.array.titles);
        authors = getResources().getStringArray(R.array.authors);
        TypedArray images = getResources().obtainTypedArray(R.array.images);
        if(titles.length>authors.length)
        {
            length = authors.length;
        }
        else
        {
            length = titles.length;
        }
        for(int i=0;i<length;i++)
        {
            Map map = new HashMap();
            map.put(NEWS_TITLE,titles[i]);
            map.put(NEWS_AUTHOR,authors[i]);
            dataList.add(map);
        }
    }
}

