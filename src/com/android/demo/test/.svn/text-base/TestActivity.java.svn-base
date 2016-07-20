package com.android.demo.test;

import com.android.demo.view.*;

import android.app.Activity;
import android.graphics.Color;
import android.os.Bundle;
import android.os.Handler;
import android.os.Message;
import android.os.SystemClock;
public class TestActivity extends Activity{

    private CurveChartView dc = null;
    
    private boolean isRun = true;
    
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
        float d = 0;
        float sp = 0.1f;
        float[] data = new float[100];
        float[] data1 = new float[100];
        float[] data2 = new float[100];
        for(int i = 0; i <100; i++){
            data[i] = (float)(Math.sin(d) *10);
            data1[i] = (float)(Math.cos(d) *5);
            data2[i] =  3*data[i]- data1[i]*data1[i] * 2 ;
            d += sp;
        }
        CurveChartView chart = (CurveChartView)findViewById(R.id.chart);
        chart.setCurveCount(3);
        
        chart.setCurveColor(new int[]{Color.YELLOW,Color.BLUE,Color.RED});
        chart.setCalibrationOn(true);
        chart.setData(0,data);
        chart.setData(1,data1);
        chart.setData(2,data2);
        
        dc = (CurveChartView)findViewById(R.id.dchart);
        dc.setCurveStatic(false);
        dc.setCurveCount(2);
        dc.setCalibrationLeft(true);
        dc.setCurveColor(new int[]{Color.BLUE,Color.YELLOW});
        dc.setCalibrationOn(true);
        dc.setCalibrationLeft(true);
        dc.setDataScope(0, 100);
        
        DataThread dt = new DataThread();
        dt.start();
      
        
        PieChartView pcv = (PieChartView)findViewById(R.id.pie);
        pcv.setDataCount(5);
        pcv.setColor(new int[]{Color.YELLOW,Color.BLUE,Color.GRAY,Color.MAGENTA,Color.RED});
        pcv.setData(new float[]{200,700,45,190,409});
        pcv.setSpecial(4);
        
        BarChartView br = (BarChartView)findViewById(R.id.bar);
        br.setGroupCount(3);
        br.setDataCount(3);
        br.setGroupData(0, new float[]{277f,2101f,3222f});
        br.setGroupData(1, new float[]{1213f,11194f,444f});
        br.setGroupData(2, new float[]{193f,2645f,858f});
        br.setBarColor(new int[]{Color.YELLOW,Color.BLUE,Color.GREEN});
        br.setDataTitle(new String[]{"±ýÍ¼²âÊÔ","Title","123234"});
        br.setGroupTitle(new String[]{"group1","group2","group3"});
    }
    
    private Handler handler = new Handler(){
        public void handleMessage(Message msg) {
            Bundle d = msg.getData();
            float d1 = d.getFloat("d1");
            float d2 = d.getFloat("d2");
            dc.appendData(new float[]{d1,d2});
        }
    };
    
    class DataThread extends Thread{
        private float d = 0;
        private float sp = 0.1f;
        
        private int t = 1;
        private boolean flat = true;
        public void run(){
            while(isRun){
            float d1 = (float)(Math.sin(d) *t);
            float d2 = (float)(Math.cos(d) * t);
            Message msg = handler.obtainMessage();
            Bundle b = new Bundle();
            b.putFloat("d1", d1);
            b.putFloat("d2", d2);
            msg.setData(b);
            handler.sendMessage(msg);
            d += sp;
            if(flat){
              t++;
              if(t > 300)
                  flat = false;
            }else{
                t--;
                if(t <= 1)
                    flat = true;
            }
            
            SystemClock.sleep(200);
            }
        }
    }
    
    public void onDestroy(){
        super.onDestroy();
        isRun = false;
    }
    
}
