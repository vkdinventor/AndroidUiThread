# AndroidUiThread
4 ways to access ui element from thread


In the viewpoint of running code in the UI thread, is there any difference between:

MainActivity.this.runOnUiThread(new Runnable() {
    public void run() {
        Log.d("UI thread", "I am the UI thread");
    }
});
or

MainActivity.this.myView.post(new Runnable() {
    public void run() {
        Log.d("UI thread", "I am the UI thread");
    }
});
and

private class BackgroundTask extends AsyncTask<String, Void, Bitmap> {
    protected void onPostExecute(Bitmap result) {
        Log.d("UI thread", "I am the UI thread");
    }
}


new Handler().post(new Runnable() {
    @Override
    public void run() {
        // Code here will run in UI thread
    }
});


private void runThread() {

    new Thread() {
        public void run() {
            while (i++ < 1000) {
                try {
                    runOnUiThread(new Runnable() {

                        @Override
                        public void run() {
                            btn.setText("#" + i);
                        }
                    });
                    Thread.sleep(300);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }.start();
}
