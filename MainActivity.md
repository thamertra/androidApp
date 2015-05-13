# androidApp


import android.content.Intent;
import android.support.v7.app.ActionBarActivity;
import android.os.Bundle;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.widget.Button;
import android.widget.CheckBox;
import android.widget.RadioButton;
import android.widget.RadioGroup;
import android.widget.SeekBar;
import android.widget.TextView;
import android.widget.Toast;


public class MainActivity extends ActionBarActivity {
    private RadioGroup radioGroupCanie;
    private RadioButton CanieRadioButton;
    private RadioGroup radioGroupDrool;
    private RadioButton droolRadioButton;
    private TextView seekBarText ;
    private Button showResult ;
    private SeekBar seekbar;
    private CheckBox checkDog;
    private CheckBox checkCat;
    private CheckBox checkParrot;
    private int dogCounter;
    private int catCounter;



    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        setup();

        seekbar = (SeekBar)findViewById(R.id.seekBarId);
        seekBarText= (TextView)findViewById(R.id.progressTextView);
        seekbar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() {
            @Override
            public void onProgressChanged(SeekBar seekBar, int i, boolean b) {
                seekBarText.setText("Confortableness : " + i + "/"+ seekBar.getMax());
            }

            @Override
            public void onStartTrackingTouch(SeekBar seekBar) {

            }

            @Override
            public void onStopTrackingTouch(SeekBar seekBar) {

            }
        });

    }

public void setup()
{
    dogCounter = 0;
    catCounter = 0;

    radioGroupCanie = (RadioGroup)findViewById(R.id.canieradioGroup);
    radioGroupDrool = (RadioGroup)findViewById(R.id.RadioGroupDrool);
    showResult = (Button)findViewById(R.id.showResultButton);

    checkDog =(CheckBox)findViewById(R.id.checkBoxDog);
    checkCat = (CheckBox)findViewById(R.id.checkBoxCat);
    checkParrot= (CheckBox)findViewById(R.id.checkBoxParrot);

    processCanie(radioGroupCanie);
    processCutest(checkCat,checkDog,checkParrot);
    processDrool(radioGroupDrool);



    showResult.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View view) {
    //     Toast.makeText(getApplicationContext(),"Dog Counter" + dogCounter + " Cat Counter "+ catCounter,Toast.LENGTH_LONG).show();

            Intent i  = new Intent(MainActivity.this,ResultActivity.class);
            i.putExtra("catCounter",catCounter);
            i.putExtra("dogCounter",dogCounter);
            startActivity(i);

        }
    });



}

    public void processCutest(final CheckBox cat,final CheckBox dog ,final CheckBox parrot)
    {
        if(dog.isChecked() && !cat.isChecked() && !parrot.isChecked())
        {
            //process
            dogCounter  += 5 ;

        }
        else  if(cat.isChecked() && !dog.isChecked() && !parrot.isChecked())
        {
            catCounter +=5  ;
        }

    }

    public void processDrool(final RadioGroup radioGroup)
    {
        radioGroup.setOnCheckedChangeListener(new RadioGroup.OnCheckedChangeListener() {
            @Override
            public void onCheckedChanged(RadioGroup radioGroup, int checkId ) {

                int RadioId = radioGroup.getCheckedRadioButtonId();
                droolRadioButton = (RadioButton)findViewById(RadioId);
                if(droolRadioButton.getText().equals("Yes"))
                {
                    dogCounter +=5;
                }

            }
        });
    }

    public void processCanie(final RadioGroup radioGroup)
    {
        radioGroup.setOnCheckedChangeListener(new RadioGroup.OnCheckedChangeListener() {
            @Override
            public void onCheckedChanged(RadioGroup radioGroup, int checkId ) {

                int RadioId = radioGroup.getCheckedRadioButtonId();
                CanieRadioButton = (RadioButton)findViewById(RadioId);
                if(CanieRadioButton.getText().equals("No"))
                {
                    catCounter +=5;
                }

            }
        });
    }


}
