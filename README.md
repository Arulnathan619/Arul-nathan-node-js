Import React, { useState } from ‘react’;
Import { Calendar, Clock, Users, Bell, Plus, Search, ChevronLeft, ChevronRight, Video, MapPin, X, Check } from ‘lucide-react’;

Export default function IBMEventScheduler() {
  Const [view, setView] = useState(‘calendar’); // calendar, list, create
  Const [selectedDate, setSelectedDate] = useState(new Date());
  Const [showCreateModal, setShowCreateModal] = useState(false);

  Const events = [
    { id: 1, title: ‘Team Standup’, time: ’09:00 AM’, duration: ’30 min’, attendees: 5, type: ‘meeting’, color: ‘blue’ },
    { id: 2, title: ‘Client Demo’, time: ’02:00 PM’, duration: ‘1 hour’, attendees: 8, type: ‘presentation’, color: ‘purple’ },
    { id: 3, title: ‘Code Review’, time: ’04:30 PM’, duration: ’45 min’, attendees: 3, type: ‘review’, color: ‘green’ }
  ];

  Const upcomingEvents = [
    { date: ‘Today’, title: ‘Team Standup’, time: ’09:00 AM’, status: ‘ongoing’ },
    { date: ‘Today’, title: ‘Client Demo’, time: ’02:00 PM’, status: ‘upcoming’ },
    { date: ‘Tomorrow’, title: ‘Sprint Planning’, time: ’10:00 AM’, status: ‘upcoming’ },
    { date: ‘Feb 25’, title: ‘Quarterly Review’, time: ’03:00 PM’, status: ‘scheduled’ }
  ];

  Return (
    <div className=”w-full h-screen bg-gray-50 flex flex-col”>
      {/* IBM Header */}
      <header className=”bg-black text-white px-6 py-4 flex items-center justify-between”>
        <div className=”flex items-center gap-3”>
          <div className=”font-bold text-2xl”>IBM</div>
          <div className=”h-6 w-px bg-gray-600”></div>
          <h1 className=”text-lg font-medium”>Event Scheduler</h1>
        </div>
        <div className=”flex items-center gap-4”>
          <button className=”p-2 hover:bg-gray-800 rounded”>
            <Bell className=”w-5 h-5” />
          </button>
          <div className=”w-8 h-8 bg-blue-600 rounded-full flex items-center justify-center text-sm font-semibold”>
            JD
          </div>
        </div>
      </header>

      <div className=”flex flex-1 overflow-hidden”>
        {/* Sidebar */}
        <aside className=”w-64 bg-white border-r border-gray-200 p-4 flex flex-col gap-4”>
          <button 
            onClick={() => setShowCreateModal(true)}
            className=”w-full bg-blue-600 text-white py-3 rounded-lg font-medium flex items-center justify-center gap-2 hover:bg-blue-700 transition”
          >
            <Plus className=”w-5 h-5” />
            Create Event
          </button>

          <div className=”space-y-1”>
            <button 
              onClick={() => setView(‘calendar’)}
              className={`w-full text-left px-4 py-2.5 rounded flex items-center gap-3 ${view === ‘calendar’ ? ‘bg-blue-50 text-blue-600’ : ‘text-gray-700 hover:bg-gray-50’}`}
            >
              <Calendar className=”w-5 h-5” />
              Calendar View
            </button>
            <button 
              onClick={() => setView(‘list’)}
              className={`w-full text-left px-4 py-2.5 rounded flex items-center gap-3 ${view === ‘list’ ? ‘bg-blue-50 text-blue-600’ : ‘text-gray-700 hover:bg-gray-50’}`}
            >
              <Clock className=”w-5 h-5” />
              Upcoming
            </button>
          </div>

          <div className=”border-t pt-4 mt-auto”>
            <h3 className=”text-xs font-semibold text-gray-500 uppercase mb-2”>My Calendars</h3>
            <div className=”space-y-2”>
              <label className=”flex items-center gap-2 text-sm”>
                <input type=”checkbox” defaultChecked className=”rounded” />
                <span className=”w-3 h-3 bg-blue-600 rounded”></span>
                Work Events
              </label>
              <label className=”flex items-center gap-2 text-sm”>
                <input type=”checkbox” defaultChecked className=”rounded” />
                <span className=”w-3 h-3 bg-purple-600 rounded”></span>
                Meetings
              </label>
              <label className=”flex items-center gap-2 text-sm”>
                <input type=”checkbox” className=”rounded” />
                <span className=”w-3 h-3 bg-green-600 rounded”></span>
                Personal
              </label>
            </div>
          </div>
        </aside>

        {/* Main Content */}
        <main className=”flex-1 overflow-auto”>
          {view === ‘calendar’ && (
            <div className=”p-6”>
              {/* Calendar Header */}
              <div className=”bg-white rounded-lg shadow-sm border border-gray-200 p-4 mb-4”>
                <div className=”flex items-center justify-between mb-4”>
                  <h2 className=”text-2xl font-semibold text-gray-800”>February 2025</h2>
                  <div className=”flex items-center gap-2”>
                    <button className=”p-2 hover:bg-gray-100 rounded”>
                      <ChevronLeft className=”w-5 h-5” />
                    </button>
                    <button className=”px-4 py-2 bg-gray-100 rounded font-medium text-sm”>Today</button>
                    <button className=”p-2 hover:bg-gray-100 rounded”>
                      <ChevronRight className=”w-5 h-5” />
                    </button>
                  </div>
                </div>

                {/* Mini Calendar Grid */}
                <div className=”grid grid-cols-7 gap-2”>
                  {[‘Sun’, ‘Mon’, ‘Tue’, ‘Wed’, ‘Thu’, ‘Fri’, ‘Sat’].map(day => (
                    <div key={day} className=”text-center text-xs font-semibold text-gray-500 py-2”>
                      {day}
                    </div>
                  ))}
                  {Array.from({ length: 28 }, (_, i) => (
                    <button
                      Key={i}
                      className={`aspect-square rounded-lg flex items-center justify-center text-sm ${
                        I === 21 ? ‘bg-blue-600 text-white font-semibold’ : ‘hover:bg-gray-100’
                      }`}
                    >
                      {I + 1}
                    </button>
                  ))}
                </div>
              </div>

              {/* Today’s Schedule */}
              <div className=”bg-white rounded-lg shadow-sm border border-gray-200 p-6”>
                <h3 className=”text-lg font-semibold mb-4”>Today’s Schedule – February 22</h3>
                <div className=”space-y-3”>
                  {events.map(event => (
                    <div key={event.id} className={`border-l-4 border-${event.color}-600 bg-${event.color}-50 p-4 rounded-r-lg`}>
                      <div className=”flex items-start justify-between”>
                        <div>
                          <h4 className=”font-semibold text-gray-800”>{event.title}</h4>
                          <div className=”flex items-center gap-4 mt-2 text-sm text-gray-600”>
                            <span className=”flex items-center gap-1”>
                              <Clock className=”w-4 h-4” />
                              {event.time} ({event.duration})
                            </span>
                            <span className=”flex items-center gap-1”>
                              <Users className=”w-4 h-4” />
                              {event.attendees} attendees
                            </span>
                          </div>
                        </div>
                        <button className=”px-4 py-2 bg-white border border-gray-300 rounded text-sm font-medium hover:bg-gray-50”>
                          Join
                        </button>
                      </div>
                    </div>
                  ))}
                </div>
              </div>
            </div>
          )}

          {view === ‘list’ && (
            <div className=”p-6”>
              <div className=”bg-white rounded-lg shadow-sm border border-gray-200”>
                <div className=”p-6 border-b”>
                  <h2 className=”text-2xl font-semibold text-gray-800”>Upcoming Events</h2>
                  <div className=”mt-4 relative”>
                    <Search className=”absolute left-3 top-1/2 transform -translate-y-1/2 w-5 h-5 text-gray-400” />
                    <input
                      Type=”text”
                      Placeholder=”Search events…”
                      className=”w-full pl-10 pr-4 py-2 border border-gray-300 rounded-lg”
                    />
                  </div>
                </div>
                <div className=”divide-y”>
                  {upcomingEvents.map((event, idx) => (
                    <div key={idx} className=”p-6 hover:bg-gray-50 transition”>
                      <div className=”flex items-center justify-between”>
                        <div className=”flex items-start gap-4”>
                          <div className=”text-center min-w-16”>
                            <div className=”text-xs text-gray-500 uppercase”>{event.date}</div>
                            <div className=”text-lg font-semibold text-gray-800”>{event.time.split(‘:’)[0]}</div>
                            <div className=”text-xs text-gray-500”>{event.time.split(‘ ‘)[1]}</div>
                          </div>
                          <div>
                            <h3 className=”font-semibold text-gray-800”>{event.title}</h3>
                            <div className=”flex items-center gap-2 mt-1 text-sm text-gray-600”>
                              <span className={`px-2 py-1 rounded text-xs font-medium ${
                                Event.status === ‘ongoing’ ? ‘bg-green-100 text-green-700’ :
                                Event.status === ‘upcoming’ ? ‘bg-blue-100 text-blue-700’ :
                                ‘bg-gray-100 text-gray-700’
                              }`}>
                                {event.status}
                              </span>
                            </div>
                          </div>
                        </div>
                        <button className=”text-blue-600 hover:text-blue-700 font-medium text-sm”>
                          View Details
                        </button>
                      </div>
                    </div>
                  ))}
                </div>
              </div>
            </div>
          )}
        </main>
      </div>

      {/* Create Event Modal */}
      {showCreateModal && (
        <div className=”fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50”>
          <div className=”bg-white rounded-lg w-full max-w-2xl max-h-[90vh] overflow-auto”>
            <div className=”p-6 border-b flex items-center justify-between”>
              <h2 className=”text-xl font-semibold”>Create New Event</h2>
              <button onClick={() => setShowCreateModal(false)} className=”p-2 hover:bg-gray-100 rounded”>
                <X className=”w-5 h-5” />
              </button>
            </div>
            <div className=”p-6 space-y-4”>
              <div>
                <label className=”block text-sm font-medium text-gray-700 mb-1”>Event Title</label>
                <input type=”text” placeholder=”Enter event title” className=”w-full px-4 py-2 border border-gray-300 rounded-lg” />
              </div>
              <div className=”grid grid-cols-2 gap-4”>
                <div>
                  <label className=”block text-sm font-medium text-gray-700 mb-1”>Date</label>
                  <input type=”date” className=”w-full px-4 py-2 border border-gray-300 rounded-lg” />
                </div>
                <div>
                  <label className=”block text-sm font-medium text-gray-700 mb-1”>Time</label>
                  <input type=”time” className=”w-full px-4 py-2 border border-gray-300 rounded-lg” />
                </div>
              </div>
              <div>
                <label className=”block text-sm font-medium text-gray-700 mb-1”>Duration</label>
                <select className=”w-full px-4 py-2 border border-gray-300 rounded-lg”>
                  <option>30 minutes</option>
                  <option>1 hour</option>
                  <option>2 hours</option>
                  <option>Custom</option>
                </select>
              </div>
              <div>
                <label className=”block text-sm font-medium text-gray-700 mb-1”>Attendees</label>
                <input type=”text” placeholder=”Add attendees by email” className=”w-full px-4 py-2 border border-gray-300 rounded-lg” />
              </div>
              <div>
                <label className=”block text-sm font-medium text-gray-700 mb-1”>Location/Link</label>
                <div className=”flex gap-2”>
                  <input type=”text” placeholder=”Add meeting link or location” className=”flex-1 px-4 py-2 border border-gray-300 rounded-lg” />
                  <button className=”p-2 border border-gray-300 rounded-lg hover:bg-gray-50”>
                    <Video className=”w-5 h-5” />
                  </button>
                </div>
              </div>
              <div>
                <label className=”block text-sm font-medium text-gray-700 mb-1”>Description</label>
                <textarea rows=”3” placeholder=”Add event description” className=”w-full px-4 py-2 border border-gray-300 rounded-lg”></textarea>
              </div>
            </div>
            <div className=”p-6 border-t bg-gray-50 flex gap-3 justify-end”>
              <button onClick={() => setShowCreateModal(false)} className=”px-6 py-2 border border-gray-300 rounded-lg font-medium hover:bg-gray-100”>
                Cancel
              </button>
              <button className=”px-6 py-2 bg-blue-600 text-white rounded-lg font-medium hover:bg-blue-700 flex items-center gap-2”>
                <Check className=”w-5 h-5” />
                Create Event
              </button>
            </div>
          </div>
        </div>
      )}
    </div>
  );
}
