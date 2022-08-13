# soccer-news-app
App nativo Android
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    package="com.calculadora.soccorviws">

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.SoccorViws"
        tools:targetApi="31">
        <activity
            android:name=".MainActivity"
            android:exported="true"
            android:label="@string/app_name">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

<package com.calculadora.soccorviws.domem;

public class News {
    private String title;
    private String descriptio;

    public News() {
        this.title = title;
        this.descriptio = descriptio;
    }

    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    public String getDescriptio() {
        return descriptio;
    }

    public void setDescriptio(String descriptio) {
        this.descriptio = descriptio;
    }
}
package com.calculadora.soccorviws.ui.adapter;

import android.view.ViewGroup;

import androidx.annotation.NonNull;
import androidx.recyclerview.widget.RecyclerView;

import com.calculadora.soccorviws.databinding.NewsTimeBinding;
import com.calculadora.soccorviws.domem.News;

import java.util.List;

public class NewsAdapter extends RecyclerView.Adapter<NewsAdapter.VienHolder> {
   private List<News> news;

   public NewsAdapter(List<News> news){
       this.news = news;

   }

    @NonNull
    @Override
    public VienHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        return null;
    }

    @Override
    public void onBindViewHolder(@NonNull VienHolder holder, int position) {
       News news = this.news.get(position);
       holder.binding.tvTitle.setText(news.getTitle());
       holder.binding.tvDescription.setText(news.getDescriptio());
    }

    @Override
    public int getItemCount() {
        return this.news.size();
    }

    public static class VienHolder extends RecyclerView.ViewHolder {

        private final NewsTimeBinding binding;

        public VienHolder(NewsTimeBinding binding) {
            super(binding.getRoot());
            this.binding = binding;
        }
    }
package com.calculadora.soccorviws.ui.favorites;

import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ImageView;

import androidx.annotation.NonNull;
import androidx.fragment.app.Fragment;
import androidx.lifecycle.Observer;
import androidx.lifecycle.ViewModelProvider;
import androidx.recyclerview.widget.LinearLayoutManager;

import com.calculadora.soccorviws.databinding.FragmentFavovitesBinding;
import com.calculadora.soccorviws.domem.News;
import com.calculadora.soccorviws.ui.adapter.NewsAdapter;

import java.util.List;

public class FavoritesFragment extends Fragment {

    private FragmentFavovitesBinding binding;

    public View onCreateView(@NonNull LayoutInflater inflater,
                             ViewGroup container, Bundle savedInstanceState) {
        FavoritesViewModel dashboardViewModel =
                new ViewModelProvider(this).get(FavoritesViewModel.class);

        binding = FragmentFavovitesBinding.inflate(inflater, container, false);
        View root = binding.getRoot();

        binding.rvNews.setlayoutManager(new LinearLayoutManager(getContext()));
        List<News> news;
        binding.rvNews.setAdaptar(new NewsAdapter(news ));


        final ImageView textView = binding.ivFavorite;
        dashboardViewModel.getText().observe(getViewLifecycleOwner(),
                (Observer<? super String>) textView);
        return root;
    }

    @Override
    public void onDestroyView() {
        super.onDestroyView();
        binding = null;
