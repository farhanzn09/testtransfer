#include "ros/ros.h"
#include "std_msgs/String.h"

int main(int argc, char **argv) {
    // Inisialisasi ROS node
    ros::init(argc, argv, "ros_to_arduino");
    ros::NodeHandle nh;

    // Buat publisher
    ros::Publisher arduino_pub = nh.advertise<std_msgs::String>("arduino_topic", 10);

    ros::Rate loop_rate(1); // Kirim data dengan kecepatan 1 Hz

    while (ros::ok()) {
        // Buat pesan
        std_msgs::String msg;
        msg.data = "Hello, Arduino from ROS!";

        // Publish pesan
        arduino_pub.publish(msg);

        // Debug log
        ROS_INFO("Sent: %s", msg.data.c_str());

        // Tunggu sesuai rate
        ros::spinOnce();
        loop_rate.sleep();
    }

    return 0;
}
