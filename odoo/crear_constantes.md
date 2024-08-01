# COMO UTILIZAR CONSTANTES EN OTRA CLASE

from .zkconst import *


def zkconnect(self):
    """Start a connection with the time clock"""
    command = CMD_CONNECT
    command_string = ''


# CREAR UNA CLASE DE CONSTANTES

from datetime import datetime, date

USHRT_MAX = 65535

CMD_CONNECT = 1000
CMD_EXIT = 1001

def encode_time(t):
    """Encode a timestamp send at the timeclock

    copied from zkemsdk.c - EncodeTime"""
    d = ( (t.year % 100) * 12 * 31 + ((t.month - 1) * 31) + t.day - 1) *\
         (24 * 60 * 60) + (t.hour * 60 + t.minute) * 60 + t.second

    return d


def decode_time(t):
    """Decode a timestamp retrieved from the timeclock

    copied from zkemsdk.c - DecodeTime"""
    second = t % 60
    t = t / 60

    minute = t % 60
    t = t / 60

    hour = t % 24
    t = t / 24

    day = t % 31+1
    t = t / 31

    month = t % 12+1
    t = t / 12

    year = t + 2000

    d = datetime(int(year), int(month), int(day), int(hour), int(minute), int(second))

    return d
    
