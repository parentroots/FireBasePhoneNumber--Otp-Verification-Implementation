# FireBasePhoneNumber--Otp-Verification-Implementation


Backer Workd 
   Go to your activity  
1==  //   

     // String sendOtpNumber=017********** number on user Send

     

               PhoneAuthProvider.getInstance().verifyPhoneNumber("+88" + sendOtpNumber, 120, TimeUnit.SECONDS, this
                       , new PhoneAuthProvider.OnVerificationStateChangedCallbacks() {
                           @Override
                           public void onVerificationCompleted(@NonNull PhoneAuthCredential phoneAuthCredential) {

                           }

                           @Override
                           public void onVerificationFailed(@NonNull FirebaseException e) {
                             
                           }

                           @Override
                           public void onCodeSent(@NonNull String verificationId, @NonNull PhoneAuthProvider.ForceResendingToken forceResendingToken) {

                               Intent intent=new Intent(SendOtpActivity.this, OtpVerifyActivity.class);
                               intent.putExtra("sendOtpNumber",sendOtpNumber);
                               intent.putExtra("verificationId",verificationId);
                               startActivity(intent);
                           }
                       }
               );



1 ==connect project on firebase
2== implement all Firebase SDK
3==go to firebase console > project setting > scrool down and fingerprint > paste SHA1 key 
4== enable authentication with number
