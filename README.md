# SendClickFromWebView
SendClickFromWebView

<!DOCTYPE html>
        <html lang="en">
        <body>
        <input type="button"  value="Say hello" onClick="showAndroidToast('OK')" />
        <input type="button"  value="hello mr.vicky" onClick="showAndroidToast('MR.VICKY')" />
        <br/><br/>

        <script type="text/javascript">
            <!-- Sending value to Android -->
            function showAndroidToast(toast) {
                AndroidInterface.showToast(toast);
            }
        </script>
        </body>
        </html>



public class MainActivity extends AppCompatActivity {
    String TAG = "MainActivity";
    WebView wvTermscondition;

    @SuppressLint("JavascriptInterface")
    @Override
    public void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_web);

        wvTermscondition = findViewById(R.id.webview1);
        wvTermscondition.loadUrl( AppSettings.restapi + "/ujianmulai?id=" + soal_jawab_id );


        wvTermscondition.setWebChromeClient(new WebChromeClient() {
            @Override
            public boolean onJsAlert(WebView view, String url, String message, JsResult result) {
                //Required functionality here
                return super.onJsAlert(view, url, message, result);
            }});
        wvTermscondition.addJavascriptInterface(new WebAppInterface(this), "AndroidInterface");
        wvTermscondition.getSettings().setJavaScriptEnabled(true);
        wvTermscondition.getSettings().setLoadsImagesAutomatically(true);
        wvTermscondition.setScrollBarStyle(View.SCROLLBARS_INSIDE_OVERLAY);

    }


    public class WebAppInterface {
        Context mContext;

        // Instantiate the interface and set the context
        WebAppInterface(Context c) {
            mContext = c;
        }

        @JavascriptInterface
        public void showToast(String toast) {
            if(toast.equalsIgnoreCase("OK")){
                Toast.makeText(mContext, toast, Toast.LENGTH_SHORT).show();
            }else if(toast.equalsIgnoreCase("MR.VICKY")){
                Toast.makeText(mContext, toast, Toast.LENGTH_SHORT).show();
            }
        }
    }

}


<?xml version="1.0" encoding="utf-8"?>
<androidx.coordinatorlayout.widget.CoordinatorLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main_content"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/colorPrimaryDark"
    android:fitsSystemWindows="true">

    <androidx.swiperefreshlayout.widget.SwipeRefreshLayout
        android:id="@+id/swipe"
        android:layout_width="match_parent"
        android:layout_height="match_parent">
        <WebView
            android:id="@+id/webview1"
            android:layout_width="match_parent"
            android:layout_height="match_parent">

        </WebView>
    </androidx.swiperefreshlayout.widget.SwipeRefreshLayout>

</androidx.coordinatorlayout.widget.CoordinatorLayout>
