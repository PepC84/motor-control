int PHASE_BLUE = 25;
int PHASE_WHITE = 35;
int PHASE_GREEN = 34;

int LOWBLUE = 16;
int HIGHBLUE = 17;

int LOWWHITE = 18;
int HIGHWHITE = 19;

int LOWGREEN = 26;
int HIGHGREEN = 27;

int PHASE_BLUE_STATE;
int PHASE_WHITE_STATE;
int PHASE_GREEN_STATE;

unsigned long lastStep;
bool bootSequence;
int waitTimeBootMicros = 100000;
int waitTimeDecreaseConst = 0;;
int bootStep = 1;
void setup() {
  setAllPins();
  Serial.begin(115200));
}

void loop() {
  Serial.print("when uhhh whe ");
  PHASE_BLUE_STATE = analogRead(PHASE_BLUE);
  PHASE_WHITE_STATE = analogRead(PHASE_WHITE);
  PHASE_GREEN_STATE = analogRead(PHASE_GREEN);
  
  Serial.print(PHASE_BLUE_STATE);
  Serial.print(PHASE_WHITE_STATE);
  Serial.println(PHASE_GREEN_STATE);
  //self starting needs custom tuning
  if(bootSequence == true) {
    if(micros() - lastStep > waitTimeBootMicros) {
      step(bootStep);
      bootStep++;
      if(bootStep == 7) {
        bootStep = 1;
      }
      waitTimeBootMicros -= waitTimeDecreaseConst;
      lastStep = micros();
    }
    if(waitTimeBootMicros < 1){
      bootSequence == false;
    }
  }
  if(bootSequence == false) {
    if(PHASE_BLUE_STATE > PHASE_GREEN_STATE && PHASE_GREEN_STATE > PHASE_WHITE_STATE && PHASE_WHITE_STATE < 2048) {
      phaseON(PHASE_BLUE);
      phaseOFF(PHASE_WHITE);
      phaseDISCONNECT(PHASE_GREEN);
    }
    if(PHASE_BLUE_STATE > PHASE_WHITE_STATE && PHASE_WHITE_STATE > PHASE_GREEN_STATE && PHASE_GREEN_STATE < 2048 ) {
      phaseON(PHASE_BLUE);
      phaseOFF(PHASE_GREEN);
      phaseDISCONNECT(PHASE_WHITE);
    }
    if(PHASE_WHITE_STATE > PHASE_BLUE_STATE && PHASE_BLUE_STATE > PHASE_GREEN_STATE && PHASE_GREEN_STATE < 2048) {
      phaseON(PHASE_WHITE);
      phaseOFF(PHASE_GREEN);
      phaseDISCONNECT(PHASE_BLUE);
    }
    if(PHASE_WHITE_STATE > PHASE_GREEN_STATE && PHASE_GREEN_STATE > PHASE_BLUE_STATE&& PHASE_BLUE_STATE < 2048) {
      phaseON(PHASE_WHITE);
      phaseOFF(PHASE_BLUE);
      phaseDISCONNECT(PHASE_GREEN);
    }
    if(PHASE_GREEN_STATE > PHASE_WHITE_STATE && PHASE_WHITE_STATE > PHASE_BLUE_STATE && PHASE_BLUE_STATE < 2048) {
      phaseON(PHASE_GREEN);
      phaseOFF(PHASE_BLUE);
      phaseDISCONNECT(PHASE_WHITE);
    }
    if(PHASE_GREEN_STATE > PHASE_BLUE_STATE && PHASE_BLUE_STATE > PHASE_WHITE_STATE && PHASE_WHITE_STATE < 2048) {
      phaseON(PHASE_GREEN);
      phaseOFF(PHASE_WHITE);
      phaseDISCONNECT(PHASE_BLUE);
    }
  }
  if(PHASE_GREEN_STATE == 0 && PHASE_GREEN_STATE == PHASE_WHITE_STATE && PHASE_BLUE_STATE == 0) {
    bootSequence = true;
  }
}
void step(int stepID) {
  switch(stepID) {
    case 1:
      phaseON(PHASE_BLUE);
      phaseOFF(PHASE_WHITE);
      phaseDISCONNECT(PHASE_GREEN);
    break;
    case 2:
      phaseON(PHASE_BLUE);
      phaseOFF(PHASE_GREEN);
      phaseDISCONNECT(PHASE_WHITE);
    break;
    case 3:
      phaseON(PHASE_WHITE);
      phaseOFF(PHASE_GREEN);
      phaseDISCONNECT(PHASE_BLUE);
    break;
    case 4:
      phaseON(PHASE_WHITE);
      phaseOFF(PHASE_BLUE);
      phaseDISCONNECT(PHASE_GREEN);
    break;
    case 5:
      phaseON(PHASE_GREEN);
      phaseOFF(PHASE_BLUE);
      phaseDISCONNECT(PHASE_WHITE);
    break;
    case 6:
      phaseON(PHASE_GREEN);
      phaseOFF(PHASE_WHITE);
      phaseDISCONNECT(PHASE_BLUE);
    break;
    case 7:
      phaseON(PHASE_BLUE);
      phaseOFF(PHASE_WHITE);
      phaseDISCONNECT(PHASE_GREEN);
      Serial.print("case 7 used");
    break;
  }
}
void phaseON(int phase){
  if(phase == PHASE_BLUE) {
    digitalWrite(LOWBLUE,LOW);
    digitalWrite(HIGHBLUE,LOW);
  } else if(phase == PHASE_GREEN) {
    digitalWrite(LOWGREEN,LOW);
    digitalWrite(HIGHGREEN,LOW);
  } else {
    digitalWrite(LOWWHITE,LOW);
    digitalWrite(HIGHWHITE,LOW);
  }
}
void phaseOFF(int phase){
  if(phase == PHASE_BLUE) {
    digitalWrite(LOWBLUE,HIGH);
    digitalWrite(HIGHBLUE,HIGH);
  } else if(phase == PHASE_GREEN) {
    digitalWrite(LOWGREEN,HIGH);
    digitalWrite(HIGHGREEN,HIGH);
  } else {
    digitalWrite(LOWWHITE,HIGH);
    digitalWrite(HIGHWHITE,HIGH);
  }
}
void phaseDISCONNECT(int phase){
    if(phase == PHASE_BLUE) {
    digitalWrite(LOWBLUE,LOW);
    digitalWrite(HIGHBLUE,HIGH);
  } else if(phase == PHASE_GREEN) {
    digitalWrite(LOWGREEN,LOW);
    digitalWrite(HIGHGREEN,HIGH);
  } else {
    digitalWrite(LOWWHITE,LOW);
    digitalWrite(HIGHWHITE,HIGH);
  }
}

void enablePin(int pin) {
  if(pin % 2 == 0) {
    digitalWrite(pin,HIGH);
  } else {
    digitalWrite(pin,LOW);
  }
}
void disablePin(int pin) {
  if(pin % 2 == 0) {
    digitalWrite(pin,LOW);
  } else {
    digitalWrite(pin,HIGH);
  }
}
void setAllPins() {
  //its a lot when i see it on setup

  pinMode(16,OUTPUT);
  pinMode(17,OUTPUT);
  pinMode(26,OUTPUT);
  pinMode(27,OUTPUT);
  pinMode(18,OUTPUT);
  pinMode(19,OUTPUT);
  //set all high side fets off.
  digitalWrite(17,HIGH);
  digitalWrite(19,HIGH);
  digitalWrite(27,HIGH);
}
