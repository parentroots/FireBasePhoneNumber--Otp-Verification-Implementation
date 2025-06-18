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



//Otp Verify Activity   




        // Intent থেকে verificationId নিই
        verificationId = getIntent().getStringExtra("verificationId");

        verifyBtn.setOnClickListener(v -> {
            String otp = edOtp.getText().toString().trim();

            if (otp.isEmpty()) {
                edOtp.setError("Enter OTP");
                return;
            }

            // OTP verify করার জন্য credential বানানো
            PhoneAuthCredential credential = PhoneAuthProvider.getCredential(verificationId, otp);

            // Firebase এ sign-in করা
            signInWithCredential(credential);
        });
    }

    private void signInWithCredential(PhoneAuthCredential credential) {
        mAuth.signInWithCredential(credential)
            .addOnCompleteListener(task -> {
                if (task.isSuccessful()) {
                    // OTP verification successful
                    Toast.makeText(this, "Login Successful", Toast.LENGTH_SHORT).show();

                    // এবার চাইলে Dashboard / Home Activity-তে পাঠাতে পারিস
                    Intent intent = new Intent(OtpVerifyActivity.this, DashboardActivity.class);
                    startActivity(intent);
                    finish();
                } else {
                    Toast.makeText(this, "Verification Failed", Toast.LENGTH_SHORT).show();
                }
            });
