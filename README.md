# safty_challenge

{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Intro\n",
    "No one likes jerky rides, we’ve been helping our driver-partners understand how they drive so they can become better drivers.\n",
    "\n",
    "By collecting GPS, gyroscope and accelerometer data from our app during Grab trips, we are able to provide our driver-partners with weekly telematics reports on their driving patterns like speeding, acceleration and braking, so they know where they can do better.\n",
    "\n",
    "Problem Appears to Sequential Problem But good Feature Engineering will turn this problem to  Structure Data Problem.  \n",
    "\n",
    "#### NOTE: This is only proof of concept, Actual Model will be implemented using Apache BEAM, will be update later in this Repo \n",
    "\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Engineered Features:\n",
    "Features are decided upon primarily through domain knowledge and analysis of correlation.\n",
    "\n",
    "|Engineered Features (Datapoint):|Description: |\n",
    "| -------------                  |---|\n",
    "|Harsh Accleration                |Harsh Accleration is Determined from acceleometer Z axis, if the accelertion is above threshold Value in m/s2.\n",
    "|Harsh Braking                   |Harsh braking is sudden Decccleration that is Determined from acceleometer Z axis,  if the accelertion is below threshold Value in m/s2\n",
    "|Harsh Turns                  |Harsh Turn is Determined from acceleometer x axis, if the accelertion is above threshold Value m/s2 in Both Direction\n",
    "|Harsh Bumps                   |Harsh Bumps is Determined from acceleometer y axis, if the accelertion is above threshold Value m/s2 in Both Direction\n",
    "|Change in Phone Orentation                   |Change in Phone orentation is determined from the change in gyro values\n",
    "|Harsh Pitch                          |Harsh Pitch is determined from difference in pitch mean value of the bookingID + pitch threshold value,  \n",
    "pitch = atan2((- acceleration_x) , sqrt(acceleration_y * acceleration_y + acceleration_z * acceleration_z)) * 57.3\n",
    "|Harsh Roll                          |Harsh Roll is determined from difference in roll mean value of the bookingID + roll hreshold value,  \n",
    "roll = atan2(y_Buff , z_Buff) * 57.3\n",
    "|Harsh Speeding(Exceding Speed Limit)                           |Speed above Treshold Values\n",
    "|Distance                     |Distance based on Time * Average Speed, Distance is used to penalize the above value based on Distance of the BookingID"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "##### Statical Feature mean, average and std deviation were added to increase the accuracy. But didn't Help. \n",
    "##### Feature is bucketies to get more accuracy "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "#### Feature Correlation Map\n",
    "\n",
    " <td> <img src=\"img/heatmap.png\" alt=\"Drawing\" style=\"width: 600px;\"/> </td>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "|FeatureData Features (Datapoint):|Description: |\n",
    "| -------------                  |---|\n",
    "|Pitch                |Correlation With Acceleration, Braking and Bumps\n",
    "|Roll                |Turns\n",
    "|Braking                |Don't Corelate with Acceleration and correlate with Pitch \n",
    "|Phone Orientation                |Correlate with Pitch Roll, Acceleration, Braking and Turns\n",
    " Did feature bucketing To increase the accuracy. \n",
    "\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "#### Final Model accuracy\n",
    "\n",
    "<td> <img src=\"img/final_model.png\" alt=\"Drawing\" style=\"width: 1000px;\"/> </td>\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "#### Conclusion\n",
    "#### Best model is gradient boosted decision tree, need more data to increase accuracy, try Deep Neural Network like LinearClassification, LinearDNNClassifier, Custom Estimators. Still we cannot increase the accuracy.\n",
    "#### Even consider bucketizing the features and added second order polynomials features, still cannot increase the accuracy. I need more data to increase accuracy and prove my hypothesis."
   ]
  }
